# S3 배포용 IAM 계정 및 권한 구성 문서

## 1. 배포 정보

- **AWS 계정 ID**: `725478842252`
- **S3 버킷**: `dev-web-ide-fe-prod-apne2`
- **리전**: `ap-southeast-2`
- **배포 URL**: http://dev-web-ide-fe-prod-apne2.s3-website-ap-southeast-2.amazonaws.com/
- **정적 웹 호스팅 설정**
  - Index document: `index.html`
  - Error document: `index.html`
- **최근 수동 재배포 일시**: `2026-09-09 11:19 KST`

## 2. 배포 방식

GitHub Actions에서 Vite 빌드 결과물인 `dist` 디렉터리를 S3 버킷 루트로 동기화합니다.

```yaml
SOURCE_DIR: './dist'
AWS_REGION: 'ap-southeast-2'
AWS_S3_BUCKET: ${{ secrets.AWS_S3_BUCKET }}
AWS_ACCESS_KEY_ID: ${{ secrets.AWS_ACCESS_KEY_ID }}
AWS_SECRET_ACCESS_KEY: ${{ secrets.AWS_SECRET_ACCESS_KEY }}
```

현재 버킷은 `BucketOwnerEnforced` 설정으로 S3 Object ACL을 허용하지 않습니다. 따라서 배포 옵션에 `--acl public-read`를 사용하지 않고, 공개 접근은 버킷 정책으로 처리합니다.

```yaml
args: --follow-symlinks --delete
```

## 3. IAM 사용자

- **IAM 사용자 이름**: `pet-travel-found-deployer`
- **IAM 사용자 ARN**: `arn:aws:iam::725478842252:user/pet-travel-found-deployer`
- **정책 이름**: `PetTravelFoundS3DeployPolicy`
- **용도**: GitHub Actions S3 배포 전용 Access Key 발급

배포용 Access Key는 프로젝트 루트의 `aws-credentials/pet-travel-found-deployer.env`에 로컬로만 저장되어 있습니다. 해당 디렉터리는 `.gitignore`에 포함되어 커밋되지 않습니다.

## 4. IAM 권한

배포 사용자는 `dev-web-ide-fe-prod-apne2` 버킷에 대해서만 목록 조회, 업로드, 조회, 삭제 권한을 갖습니다.

```json
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Sid": "AllowListTargetBucket",
      "Effect": "Allow",
      "Action": "s3:ListBucket",
      "Resource": "arn:aws:s3:::dev-web-ide-fe-prod-apne2"
    },
    {
      "Sid": "AllowDeployObjects",
      "Effect": "Allow",
      "Action": [
        "s3:GetObject",
        "s3:PutObject",
        "s3:DeleteObject"
      ],
      "Resource": "arn:aws:s3:::dev-web-ide-fe-prod-apne2/*"
    }
  ]
}
```

## 5. GitHub Secrets

GitHub Actions 배포를 위해 repository secrets에 아래 값을 등록합니다.

```bash
AWS_S3_BUCKET=dev-web-ide-fe-prod-apne2
AWS_ACCESS_KEY_ID=<pet-travel-found-deployer access key id>
AWS_SECRET_ACCESS_KEY=<pet-travel-found-deployer secret access key>
```

`AWS_REGION`은 workflow 파일에 `ap-southeast-2`로 고정되어 있습니다.

## 6. 수동 배포 명령

로컬에서 동일한 방식으로 배포하려면 아래 명령을 사용합니다.

```bash
pnpm build
set -a
source aws-credentials/pet-travel-found-deployer.env
set +a
aws s3 sync dist s3://dev-web-ide-fe-prod-apne2/ --follow-symlinks --delete
```

배포 확인:

```bash
curl -I http://dev-web-ide-fe-prod-apne2.s3-website-ap-southeast-2.amazonaws.com/
```

정상 배포 시 `HTTP/1.1 200 OK`를 반환합니다.
