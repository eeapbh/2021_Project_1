Vue 프로젝트에 Font Awesome 패키지 설치하기



```
$ yarn add -D @fortawesome/fontawesome-svg-core 
$ yarn add -D @fortawesome/free-solid-svg-icons 
$ yarn add -D @fortawesome/vue-fontawesome
```

기본적으로 `fontawesome-svg-core`와 `vue-fontawesome`는 반드시 설치를 해야 합니다.
`fontawesome-svg-core`는 Fontawesome의 SVG파일을 던져주는 역활을 하고 `vue-fontawesome`는 던져준 SVG파일을 Vue에서 사용할 수 있게 해주는 역활을 합니다.
`free-solid-svg-icons`는 아이콘의 모음이라고 보시면 됩니다. 만약 브랜드 로고 아이콘을 사용해야 한다면 `free-brands-svg-icons`도 설치해야 하는 식입니다.

아래는 **무료**로 사용할 수 있는 아이콘 파일 모음 입니다.

```
$ yarn add @fortawesome/free-solid-svg-icons 
$ yarn add @fortawesome/free-brands-svg-icons 
$ yarn add @fortawesome/free-regular-svg-icons
```





```
main.js
//fort-awesome
import { library } from '@fortawesome/fontawesome-svg-core'
import { faUserSecret } from '@fortawesome/free-solid-svg-icons'
import { FontAwesomeIcon } from '@fortawesome/vue-fontawesome'

library.add(faUserSecret)

Vue.component('font-awesome-icon', FontAwesomeIcon)

Vue.config.productionTip = false
```