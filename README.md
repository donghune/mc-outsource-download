# mc-outsource-download

[mc-outsource](https://github.com/donghune/mc-outsource)(비공개) 외주 런처들의 **배포 전용** 공개 저장소. 소스는 없다. 여기 파일은 손으로 고치지 말고 mc-outsource/launcher 의 스크립트로만 갱신한다.

```
mc-outsource-download/
└── <client-id>/
    ├── distribution.json        # 런처가 읽는 모드팩 인덱스        ← npm run publish-distro
    ├── files/                   # 모드 jar, Fabric 매니페스트, seed 파일 (이름에 md5 접두)
    └── launcher/
        └── latest*.yml          # 이 클라이언트 런처의 자동 업데이트 피드  ← npm run release
```

- 런처 설치 파일은 **Releases**에 있다. 태그: `<client-id>-v<version>`
- 클라이언트마다 피드가 따로라서, 한 저장소를 같이 써도 다른 클라이언트의 릴리즈로 업데이트되지 않는다.

## 갱신 (mc-outsource/launcher 에서)

```bash
CLIENT=<id> npm run distro && CLIENT=<id> npm run publish-distro   # 모드팩
CLIENT=<id> npm run dist:win && CLIENT=<id> npm run release         # 런처
```

자세한 규칙은 mc-outsource 의 `launcher/README.md` 참고.
