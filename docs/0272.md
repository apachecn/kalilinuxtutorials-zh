# Heap hopper——堆实现的有界模型检查框架

> 原文：<https://kalilinuxtutorials.com/heaphopper/>

eapHopper 是一个用于堆实现的有界模型检查框架。

## **堆料机设置**

```
sudo apt update && sudo apt install build-essential python-dev virtualenvwrapper
git clone https://github.com/angr/heaphopper.git && cd ./heaphopper
mkvirtualenv -ppython2 heaphopper
pip install -e .
```

#### **所需套餐**

```
build-essential python-dev virtualenvwrapper
```

#### **所需的 Python-Packages**

```
ana angr cle claripy IPython psutil pyelftools pyyaml
```

**也读[DarkSpiritz——一个针对 UNIX 系统的渗透测试框架](https://kalilinuxtutorials.com/darkspiritz-penetration-testing/)**

## **例题**

```
# Gen zoo of permutations
heaphopper.py gen -c analysis.yaml

#  Trace instance
make -C tests
heaphopper.py  trace -c tests/how2heap_fastbin_dup/analysis.yaml -b tests/how2heap_fastbin_dup/fastbin_dup.bin

# Gen PoC
heaphopper.py poc -c tests/how2heap_fastbin_dup/analysis.yaml -r tests/how2heap_fastbin_dup/fastbin_dup.bin-result.yaml -d tests/how2heap_fastbin_dup/fastbin_dup.bin-desc.yaml -s tests/how2heap_fastbin_dup/fastbin_dup.c -b tests/how2heap_fastbin_dup/fastbin_dup.bin

# Tests
cd tests
# Show source
cat how2heap_fastbin_dup/fastbin_dup.c
# Run tests
./run_tests.py
# Show PoC source
cat pocs/malloc_non_heap/fastbin_dup.bin/poc_0_0.c
# Run PoC
./run_poc.sh pocs/malloc_non_heap/fastbin_dup.bin/bin/poc_0_0.bin
```

[![](img/d861a9096555aeb1980fc054015933d7.png)](https://github.com/angr/heaphopper)