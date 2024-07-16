### Process

1. python3.11로 상향
```bash
brew install python@3.11
ln -s -f /opt/homebrew/bin/python3.11 /opt/homebrew/bin/python
ln -s -f /opt/homebrew/bin/python3.11 /opt/homebrew/bin/python3
(python3 경로는 하단)
```

2. conda environment: 가상환경
```bash
conda create --name llama3 python=3.11 
conda activate llama3
```

3. 허깅페이스 CLI
```bash
pip3 install -U "huggingface_hub[cli]" 
huggingface-cli login
```

4. Git LFS: 파일포인터이용 대용량파일처리
```bash
brew install git-lfs
git lfs  
```

5. llama3-8b clone
```bash
git lfs install
git clone https://huggingface.co/meta-llama/Meta-Llama-3-8B-Instruct
```

6. llama.cpp
```bash
git clone https://github.com/ggerganov/llama.cpp 
cd llama.cpp 
LLAMA_METAL=1 make # mac m1 MPS 사용중
python3 -m pip install -r requirements.txt
```

8. 허깅페이스 모델을 llama.cpp 이 사용가능한 형태로
```bash
python3 convert-hf-to-gguf.py /Users/aiden-kwak/Web/FirstLlama3/Meta-Llama-3-8B-Instruct
```

9. quantize f16 to q4

```bash
./llama-quantize /folder/Meta-Llama-3-8B-Instruct/ggml-model-f16.gguf q4_0
```

10. run model
```bash
./llama-cli -m /Users/aiden-kwak/Web/FirstLlama3/Meta-Llama-3-8B-Instruct/ggml-model-Q4_0.gguf -n 256 --repeat_penalty 1.0 --color -i -r "User:" -f prompts/chat-with-bob.txt
```

### deprecation-warning 발생시 참고:
https://github.com/ggerganov/llama.cpp/blob/master/examples/deprecation-warning/README.md
