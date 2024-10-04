# leakschecker

C言語のmallocが正常にfreeされているかどうか確認するためのものです

`malloc`と`free`がそれぞれ`leak_detect_malloc`と`leak_detect_check`に読み替えられます

main関数のあるファイルの先頭に以下を記入して，`leakdetect.c`と`leakdetect.h`と一緒にコンパイルしてください
```c
#include "leakdetect.h"

#define LEAK_DETECT
#ifdef LEAK_DETECT
# define init leak_detect_init
# define malloc(s) leak_detelc_malloc(s, __FILE__, __LINE__)
# define free leak_detect_free
# define check leak_detect_check
#else
# define init()
# define check()
#endif
```