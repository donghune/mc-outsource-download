# mc-outsource-download

[mc-outsource](https://github.com/donghune/mc-outsource)(비공개) 외주 런처들의 **배포 전용** 공개 저장소. 소스는 없다.

```
mc-outsource-download/
└── <client-id>/                 # launcher/dist-distro/<client-id>/ 를 그대로 복사
    ├── distribution.json        # 런처가 읽는 모드팩 인덱스
    └── files/                   # 모드 jar, Fabric 매니페스트, seed 파일 (이름에 md5 접두가 붙음)
```

- 클라이언트의 `distro.json` → `"baseUrl": "https://raw.githubusercontent.com/donghune/mc-outsource-download/main/<client-id>/"`
- 클라이언트의 `client.json` → `"distributionUrl": "<위 baseUrl>distribution.json"`
- 런처 설치 파일은 **Releases**에 올린다 (100MB 넘는 파일은 저장소에 못 넣음). 태그: `<client-id>-v<version>`

## 갱신 절차

```bash
# mc-outsource/launcher 에서
CLIENT=<id> npm run distro
rsync -a --delete dist-distro/<id>/ ../../mc-outsource-download/<id>/
# 여기서 커밋·푸시
```

- 파일 이름에 해시가 붙어 있어서 raw CDN 캐시(수 분) 때문에 옛 jar를 받는 일은 없다. `distribution.json` 자체는 캐시 때문에 몇 분 늦게 반영될 수 있다.
- 이미 올라간 파일을 같은 이름으로 덮어쓰지 않는다.
- jar 하나가 100MB를 넘으면 저장소에 못 올리니 그 파일만 Releases에 올리고 `distro.json`에서 `{"url": ...}`로 참조한다.
