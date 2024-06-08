# magicoder-test
- KT Cloud 에서 `Magicoder: Source Code Is All You Need` 레포지토리의 코드를 테스트한 과정을 기록한 문서입니다.

## 세션 생성
- 거의 디폴트 설정을 그대로 두되 메인 메모리 등은 할당가능한 최대값으로 하였습니다. (짜투리 남겨 둬봤자 쓸모가 없음)
- 미리 만들어 두었던 `.dataset`, `.model`, `.code` 폴더는 자동 선택되어 세션에 마운트 됩니다.
    ![alt text](image.png)

## 개발 환경 접속과 설정
- 콘솔, VS code, Jupyter 등이 무엇으로 해도 별 차이는 없습니다. (본인 편한 것으로 진행)
- (**주의: NFS 폴더로 캐시 폴더를 변경하면 다운로드하면서 file lock에서 먹통이 되는 현상이 있다고 합니다. 만약 그렇다면 `unset HF_HOME`을 하여 export 한 것을 취소하고 캐시 폴더가 너무 커지지 않게 관찰하면서 실행해야 합니다.**) 실행 중 모델이나 데이터셋을 허깅페이스에서 다운로드 받으면 ~/.cache/huggingface 에 저장하여 (루트 파티션이 충분히 크지 않아서) 저장 공간이 부족합니다. 그나마 여유가 있는 폴더로 디폴트 폴더를 변경합니다.
    ```bash
    export HF_HOME='~/.model'
    ```
- 허깅페이스로 로그인을 해둡니다. (로그인에 필요한 접속 토크는 허깅페이스에 회원 가입하여 설정 메뉴에서 생성할 수 있습니다.)
    ```bash
    huggingface-cli login
    ```
- 실행할 코드를 저장할 폴더를 만듭니다.
    ```bash 
    cd .code
    mkdir 4x4
    cd 4x4
    ```

## 레포지토리 가져오고 데모 돌려보기
- 레포지토리에서 코드를 받아온다.
    ```bash
    git clone https://github.com/ise-uiuc/magicoder.git
    cd magicoder/
    ```
- 데모 프로그램을 돌려본다. (안 해보셔도 됨)
    ```bash
    cd demo
    pip install gradio
    pip install -U bitsandbytes
    CUDA_VISIBLE_DEVICES=0 python magicoder_demo.py --base_model "ise-uiuc/Magicoder-S-DS-6.7B" --device "cuda:0" --port 8080
    ```
- 모델이 다운로드가 되고 gradio가 실행되면 이런 메시지가 나오는데 아무데서나 웹 브라우저로 아래의 임시 링크로 접속하면 된다. 프로그래밍 질문을 던져서 잘 푸는지 본다.
![alt text](image-1.png)

