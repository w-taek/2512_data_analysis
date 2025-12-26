# GitHub 인증(HTTPS PAT vs SSH) & known_hosts 이슈

## 증상
- remote: Invalid username or token. Password authentication is not supported...
- The authenticity of host 'github.com (...)' can't be established...
- Host key verification failed

## 원인
- HTTPS는 비밀번호 인증 불가 → PAT 필요
- SSH는 첫 접속 시 호스트키를 known_hosts에 등록해야 함

## 해결(내가 한 절차)
1) origin을 SSH로 변경
2) ssh-agent에 키 등록
3) github.com 호스트키 등록(yes)
4) push 성공

## 재발 방지 체크
- 원격 URL: `git@github.com:...` 확인
- `ssh -T git@github.com`로 인증 확인
- 충돌 시 `ssh-keygen -R github.com` 후 재시도