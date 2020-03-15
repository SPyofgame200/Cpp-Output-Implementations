----------
**Purpose:**
---------- 

- First, sorry for my bad English.
- Second, I know there are lots of topics about this. But after solving a problem that need FastIO, I feel interested in FastIO and decide to do the implementations and comparing them. But it maybe time-consuming so I make this post for ones who maybe try to find the Effeciency-Simple-IO, so you can save time instead of searching more.
- Third, usually it is need not to use FastIO. In the contest, they usually have twice or more time of the solutions code than the given time limitation. Dont worry about faster IO if it is not needed, you should improve your algorithms first, maybe you can use Bitwise Operations for x8 x32 x64 faster.
- Fourth, if the problem need to be solve in O(n) ~ O(n log n), and your algorithms work in O(n ^ 2), this Micro-Optimization doesnt help you at all (maybe you will get some more points but hard get AC), you should change the algorithms for further approach.
- Final, for some problems that needed to be solved by FastIO, you can use the suitable template and modify it for your solving the problem. Dont use the template if you dont really know how to use (I may add a guide path to the post in the future)
- Conclusion, this post is about comparing the implementations for each version of C++ language and you should choose the most suitable for you.





Here are some implementations to output numbers I found
------------------------------------------------------





**Time to write first 10.000.000 non-negative numbers**

_(base on [Codeforces Custom Test](https://codeforces.com/problemset/customtest) // GNU G++ 17 7.3.0 // GNU G++ 14 6.4.0 // GNU G++ 11 5.1.0)_

<spoiler summary="Sort by GNU G++ 17 7.3.0">

<spoiler summary="Putchar Non-recursive Dividing Implementation: 3649ms">
~~~~~
#include <iostream>

using namespace std;

inline void writeInt(int x)
{
    if (x < 0) putchar('-'), x = -x;
    int p = 1;
    for (int t = x / 10; t > 0; t /= 10)
        p *= 10;
    for (; p > 0; x %= p, p /= 10)
        putchar(x / p + '0');
}

int main()
{
    int q = 1e7;
    while (q--) writeInt(q);
    return 0;
}
~~~~~
</spoiler>





<spoiler summary="Putchar Recursive Implementation: 3510ms">
~~~~~
#include <iostream>

using namespace std;

inline void writeRec(int n) {
    if (n > 9) writeRec(n / 10);
    putchar(char(n % 10 + '0'));
}

inline void writeInt(int x)
{
    if (x < 0) putchar('-'), x = -x;
    writeRec(x);
}

int main()
{
    int q = 1e7;
    while (q--) writeInt(q);
    return 0;
}
~~~~~
</spoiler>





<spoiler summary="Putchar Reverse Implementation: 3462ms">
~~~~~
#include <iostream>

using namespace std;

#define pc putchar
inline void writeInt(int n)
{
    if (n < 0) pc('-'), n = -n;
    if (!n) return (void)pc('0');
    int t = n, cnt = 0, rev = 0;
    while (!(t%10)) { cnt++; t /= 10;}
    do {rev=rev*10 + n%10;} while(n /= 10); 
    do {pc(rev % 10 + 48);} while(rev /= 10);
    while (cnt--) pc('0');
}

int main()
{
    int q = 1e7;
    while (q--) writeInt(q);
    return 0;
}
~~~~~
</spoiler>





<spoiler summary="Putchar Non-recursive toString Implementation: 3369ms">
~~~~~
#include <iostream>

using namespace std;

char os[20];
inline void writeInt(int n)
{
    if (n < 0) putchar('-'), n = -n;
    int i=0;
    do os[i++] = n%10; while(n/=10);
    while (i--) putchar(os[i] + 48);
}

int main()
{
    int q = 1e7;
    while (q--) writeInt(q);
    return 0;
}
~~~~~
</spoiler>




<spoiler summary="Printf Implementation: 1762ms">
~~~~~
#include <cstdio>

using namespace std;

int main()
{
    int q = 1e7;
    while (q--) printf("%d", q);
    return 0;
}
~~~~~
</spoiler>





<spoiler summary="synchronized(off) Cout Implementation: 1356ms">
~~~~~
#include <iostream>

using namespace std;

int main()
{
    ios::sync_with_stdio(NULL),cin.tie(NULL),cout.tie(NULL);
    int q = 1e7;
    while (q--) cout << q;
    return 0;
}
~~~~~
</spoiler>





<spoiler summary="synchronized(true) Cout Implementation: 1060ms">
~~~~~
#include <iostream>

using namespace std;

int main()
{
    ios::sync_with_stdio(true),cin.tie(NULL),cout.tie(NULL);
    int q = 1e7;
    while (q--) cout << q;
    return 0;
}
~~~~~
</spoiler>





<spoiler summary="Normal Cout Implementation: 1045ms">
~~~~~
#include <iostream>

using namespace std;

int main()
{
    int q = 1e7;
    while (q--) cout << q;
    return 0;
}
~~~~~
</spoiler>





<spoiler summary="Unlocked-Putchar Non-recursive Dividing Implementation: 919ms">
~~~~~
#include <iostream>

using namespace std;

inline void writeInt(int x)
{
    if (x < 0) _putchar_nolock('-'), x = -x;
    int p = 1;
    for (int t = x / 10; t > 0; t /= 10)
        p *= 10;
    for (; p > 0; x %= p, p /= 10)
        _putchar_nolock(x / p + '0');
}

int main()
{
    int q = 1e7;
    while (q--) writeInt(q);
    return 0;
}
~~~~~
</spoiler>





<spoiler summary="Unlocked-Putchar Reverse Implementation: 842ms">
~~~~~
#include <iostream>

using namespace std;

#define pc _putchar_nolock
inline void writeInt(int n)
{
    if (n < 0) pc('-'), n = -n;
    if (!n) return (void)pc('0');
    int t = n, cnt = 0, rev = 0;
    while (!(t%10)) { cnt++; t /= 10;}
    do {rev=rev*10 + n%10;} while(n /= 10); 
    do {pc(rev % 10 + 48);} while(rev /= 10);
    while (cnt--) pc('0');
}

int main()
{
    int q = 1e7;
    while (q--) writeInt(q);
    return 0;
}
~~~~~
</spoiler>





<spoiler summary="Unlocked-Putchar Recursive Implementation: 701ms">
~~~~~
#include <iostream>

using namespace std;

inline void writeRec(int n) {
    if (n > 9) writeRec(n / 10);
    _putchar_nolock(char(n % 10 + '0'));
}

inline void writeInt(int x)
{
    if (x < 0) _putchar_nolock('-'), x = -x;
    writeRec(x);
}

int main()
{
    int q = 1e7;
    while (q--) writeInt(q);
    return 0;
}
~~~~~
</spoiler>





<spoiler summary="Unlocked-Putchar Non-recursive toString Implementation: 670ms">
~~~~~
#include <iostream>

using namespace std;

char os[20];
inline void writeInt(int n)
{
    if (n < 0) _putchar_nolock('-'), n = -n;
    int i=0;
    do os[i++] = n%10; while(n/=10);
    while (i--) _putchar_nolock(os[i] + 48);
}

int main()
{
    int q = 1e7;
    while (q--) writeInt(q);
    return 0;
}
~~~~~
</spoiler>





<spoiler summary="fwrite buffer Implementation: 545ms">
~~~~~
#include <iostream>

using namespace std;

static const int buf_len = (1 << 14);
static const int buf_max = (1 << 04);
static char buf_out[buf_len];
static char buf_num[buf_max];
static int buf_pos = 0;

inline void writeChar(int x) {
    if (buf_pos == buf_len) fwrite(buf_out, 1, buf_len, stdout), buf_pos = 0;
    buf_out[buf_pos++] = x;
}

inline void writeInt(int x, char end = 0) {
    if (x < 0) writeChar('-'), x = -x;
    int n = 0;
    do buf_num[n++] = x % 10 + '0'; while(x /= 10);
    while (n--) writeChar(buf_num[n]);
    if (end) writeChar(end);
}

struct Flusher{~Flusher(){if(buf_pos)fwrite(buf_out, 1, buf_pos, stdout),buf_pos=0;}}flusher;

int main()
{
    int q = 1e7;
    while (q--) writeInt(q); Flusher();
    return 0;
}
~~~~~
</spoiler>

</spoiler>













































<spoiler summary="Sort by GNU G++ 14 6.4.0">

<spoiler summary="Putchar Non-recursive Dividing Implementation: 3525ms">
~~~~~
#include <iostream>

using namespace std;

inline void writeInt(int x)
{
    if (x < 0) putchar('-'), x = -x;
    int p = 1;
    for (int t = x / 10; t > 0; t /= 10)
        p *= 10;
    for (; p > 0; x %= p, p /= 10)
        putchar(x / p + '0');
}

int main()
{
    int q = 1e7;
    while (q--) writeInt(q);
    return 0;
}
~~~~~
</spoiler>





<spoiler summary="Putchar Reverse Implementation: 3447ms">
~~~~~
#include <iostream>

using namespace std;

#define pc putchar
inline void writeInt(int n)
{
    if (n < 0) pc('-'), n = -n;
    if (!n) return (void)pc('0');
    int t = n, cnt = 0, rev = 0;
    while (!(t%10)) { cnt++; t /= 10;}
    do {rev=rev*10 + n%10;} while(n /= 10); 
    do {pc(rev % 10 + 48);} while(rev /= 10);
    while (cnt--) pc('0');
}

int main()
{
    int q = 1e7;
    while (q--) writeInt(q);
    return 0;
}
~~~~~
</spoiler>





<spoiler summary="Putchar Recursive Implementation: 3354ms">
~~~~~
#include <iostream>

using namespace std;

inline void writeRec(int n) {
    if (n > 9) writeRec(n / 10);
    putchar(char(n % 10 + '0'));
}

inline void writeInt(int x)
{
    if (x < 0) putchar('-'), x = -x;
    writeRec(x);
}

int main()
{
    int q = 1e7;
    while (q--) writeInt(q);
    return 0;
}
~~~~~
</spoiler>





<spoiler summary="Putchar Non-recursive toString Implementation: 3353ms">
~~~~~
#include <iostream>

using namespace std;

char os[20];
inline void writeInt(int n)
{
    if (n < 0) putchar('-'), n = -n;
    int i=0;
    do os[i++] = n%10; while(n/=10);
    while (i--) putchar(os[i] + 48);
}

int main()
{
    int q = 1e7;
    while (q--) writeInt(q);
    return 0;
}
~~~~~
</spoiler>




<spoiler summary="Printf Implementation: 1669ms">
~~~~~
#include <cstdio>

using namespace std;

int main()
{
    int q = 1e7;
    while (q--) printf("%d", q);
    return 0;
}
~~~~~
</spoiler>





<spoiler summary="synchronized(off) Cout Implementation: 1356ms">
~~~~~
#include <iostream>

using namespace std;

int main()
{
    ios::sync_with_stdio(NULL),cin.tie(NULL),cout.tie(NULL);
    int q = 1e7;
    while (q--) cout << q;
    return 0;
}
~~~~~
</spoiler>





<spoiler summary="synchronized(true) Cout Implementation: 1091ms">
~~~~~
#include <iostream>

using namespace std;

int main()
{
    ios::sync_with_stdio(true),cin.tie(NULL),cout.tie(NULL);
    int q = 1e7;
    while (q--) cout << q;
    return 0;
}
~~~~~
</spoiler>





<spoiler summary="Normal Cout Implementation: 1075ms">
~~~~~
#include <iostream>

using namespace std;

int main()
{
    int q = 1e7;
    while (q--) cout << q;
    return 0;
}
~~~~~
</spoiler>





<spoiler summary="Unlocked-Putchar Non-recursive Dividing Implementation: 888ms">
~~~~~
#include <iostream>

using namespace std;

inline void writeInt(int x)
{
    if (x < 0) _putchar_nolock('-'), x = -x;
    int p = 1;
    for (int t = x / 10; t > 0; t /= 10)
        p *= 10;
    for (; p > 0; x %= p, p /= 10)
        _putchar_nolock(x / p + '0');
}

int main()
{
    int q = 1e7;
    while (q--) writeInt(q);
    return 0;
}
~~~~~
</spoiler>





<spoiler summary="Unlocked-Putchar Reverse Implementation: 685ms">
~~~~~
#include <iostream>

using namespace std;

#define pc _putchar_nolock
inline void writeInt(int n)
{
    if (n < 0) pc('-'), n = -n;
    if (!n) return (void)pc('0');
    int t = n, cnt = 0, rev = 0;
    while (!(t%10)) { cnt++; t /= 10;}
    do {rev=rev*10 + n%10;} while(n /= 10); 
    do {pc(rev % 10 + 48);} while(rev /= 10);
    while (cnt--) pc('0');
}

int main()
{
    int q = 1e7;
    while (q--) writeInt(q);
    return 0;
}
~~~~~
</spoiler>





<spoiler summary="Unlocked-Putchar Recursive Implementation: 561ms">
~~~~~
#include <iostream>

using namespace std;

inline void writeRec(int n) {
    if (n > 9) writeRec(n / 10);
    _putchar_nolock(char(n % 10 + '0'));
}

inline void writeInt(int x)
{
    if (x < 0) _putchar_nolock('-'), x = -x;
    writeRec(x);
}

int main()
{
    int q = 1e7;
    while (q--) writeInt(q);
    return 0;
}
~~~~~
</spoiler>





<spoiler summary="Unlocked-Putchar Non-recursive toString Implementation: 546ms">
~~~~~
#include <iostream>

using namespace std;

char os[20];
inline void writeInt(int n)
{
    if (n < 0) _putchar_nolock('-'), n = -n;
    int i=0;
    do os[i++] = n%10; while(n/=10);
    while (i--) _putchar_nolock(os[i] + 48);
}

int main()
{
    int q = 1e7;
    while (q--) writeInt(q);
    return 0;
}
~~~~~
</spoiler>





<spoiler summary="fwrite buffer Implementation: 498ms">
~~~~~
#include <iostream>

using namespace std;

static const int buf_len = (1 << 14);
static const int buf_max = (1 << 04);
static char buf_out[buf_len];
static char buf_num[buf_max];
static int buf_pos = 0;

inline void writeChar(int x) {
    if (buf_pos == buf_len) fwrite(buf_out, 1, buf_len, stdout), buf_pos = 0;
    buf_out[buf_pos++] = x;
}

inline void writeInt(int x, char end = 0) {
    if (x < 0) writeChar('-'), x = -x;
    int n = 0;
    do buf_num[n++] = x % 10 + '0'; while(x /= 10);
    while (n--) writeChar(buf_num[n]);
    if (end) writeChar(end);
}

struct Flusher{~Flusher(){if(buf_pos)fwrite(buf_out, 1, buf_pos, stdout),buf_pos=0;}}flusher;

int main()
{
    int q = 1e7;
    while (q--) writeInt(q); Flusher();
    return 0;
}
~~~~~
</spoiler>

</spoiler>













































<spoiler summary="Sort by GNU G++ 11 5.1.0">

<spoiler summary="synchronized(off) Cout Implementation: 2901ms">
~~~~~
#include <iostream>

using namespace std;

int main()
{
    ios::sync_with_stdio(NULL),cin.tie(NULL),cout.tie(NULL);
    int q = 1e7;
    while (q--) cout << q;
    return 0;
}
~~~~~
</spoiler>





<spoiler summary="synchronized(true) Cout Implementation: 2901ms">
~~~~~
#include <iostream>

using namespace std;

int main()
{
    ios::sync_with_stdio(true),cin.tie(NULL),cout.tie(NULL);
    int q = 1e7;
    while (q--) cout << q;
    return 0;
}
~~~~~
</spoiler>





<spoiler summary="Normal Cout Implementation: 2900ms">
~~~~~
#include <iostream>

using namespace std;

int main()
{
    int q = 1e7;
    while (q--) cout << q;
    return 0;
}
~~~~~
</spoiler>




<spoiler summary="Printf Implementation: 1918ms">
~~~~~
#include <cstdio>

using namespace std;

int main()
{
    int q = 1e7;
    while (q--) printf("%d", q);
    return 0;
}
~~~~~
</spoiler>





<spoiler summary="Putchar Non-recursive Dividing Implementation: 795ms">
~~~~~
#include <iostream>

using namespace std;

inline void writeInt(int x)
{
    if (x < 0) putchar('-'), x = -x;
    int p = 1;
    for (int t = x / 10; t > 0; t /= 10)
        p *= 10;
    for (; p > 0; x %= p, p /= 10)
        putchar(x / p + '0');
}

int main()
{
    int q = 1e7;
    while (q--) writeInt(q);
    return 0;
}
~~~~~
</spoiler>





<spoiler summary="Putchar Reverse Implementation: 592ms">
~~~~~
#include <iostream>

using namespace std;

#define pc putchar
inline void writeInt(int n)
{
    if (n < 0) pc('-'), n = -n;
    if (!n) return (void)pc('0');
    int t = n, cnt = 0, rev = 0;
    while (!(t%10)) { cnt++; t /= 10;}
    do {rev=rev*10 + n%10;} while(n /= 10); 
    do {pc(rev % 10 + 48);} while(rev /= 10);
    while (cnt--) pc('0');
}

int main()
{
    int q = 1e7;
    while (q--) writeInt(q);
    return 0;
}
~~~~~
</spoiler>





<spoiler summary="Putchar Non-recursive toString Implementation: 451ms">
~~~~~
#include <iostream>

using namespace std;

char os[20];
inline void writeInt(int n)
{
    if (n < 0) putchar('-'), n = -n;
    int i=0;
    do os[i++] = n%10; while(n/=10);
    while (i--) putchar(os[i] + 48);
}

int main()
{
    int q = 1e7;
    while (q--) writeInt(q);
    return 0;
}
~~~~~
</spoiler>





<spoiler summary="Putchar Recursive Implementation: 389ms">
~~~~~
#include <iostream>

using namespace std;

inline void writeRec(int n) {
    if (n > 9) writeRec(n / 10);
    putchar(char(n % 10 + '0'));
}

inline void writeInt(int x)
{
    if (x < 0) putchar('-'), x = -x;
    writeRec(x);
}

int main()
{
    int q = 1e7;
    while (q--) writeInt(q);
    return 0;
}
~~~~~
</spoiler>





<spoiler summary="fwrite buffer Implementation: 405ms">
~~~~~
#include <iostream>

using namespace std;

static const int buf_len = (1 << 14);
static const int buf_max = (1 << 04);
static char buf_out[buf_len];
static char buf_num[buf_max];
static int buf_pos = 0;

inline void writeChar(int x) {
    if (buf_pos == buf_len) fwrite(buf_out, 1, buf_len, stdout), buf_pos = 0;
    buf_out[buf_pos++] = x;
}

inline void writeInt(int x, char end = 0) {
    if (x < 0) writeChar('-'), x = -x;
    int n = 0;
    do buf_num[n++] = x % 10 + '0'; while(x /= 10);
    while (n--) writeChar(buf_num[n]);
    if (end) writeChar(end);
}

struct Flusher{~Flusher(){if(buf_pos)fwrite(buf_out, 1, buf_pos, stdout),buf_pos=0;}}flusher;

int main()
{
    int q = 1e7;
    while (q--) writeInt(q); Flusher();
    return 0;
}
~~~~~
</spoiler>

</spoiler>



















































































































































































































**Time to write 1.000 times first 10000 numbers**

_(base on [Codeforces Custom Test](https://codeforces.com/problemset/customtest) // GNU G++ 17 7.3.0 // GNU G++ 14 6.4.0 // GNU G++ 11 5.1.0)_

<spoiler summary="Sort by GNU G++ 17 7.3.0">

<spoiler summary="Putchar Reverse Implementation: 1981ms">
~~~~~
#include <iostream>

using namespace std;

#define pc putchar
inline void writeInt(int n)
{
    if (n < 0) pc('-'), n = -n;
    if (!n) return (void)pc('0');
    int t = n, cnt = 0, rev = 0;
    while (!(t%10)) { cnt++; t /= 10;}
    do {rev=rev*10 + n%10;} while(n /= 10); 
    do {pc(rev % 10 + 48);} while(rev /= 10);
    while (cnt--) pc('0');
}

int main()
{
    int q = 1e3;
    while (q--)
        for (int i = 0; i <= 1e4; ++i)
            writeInt(i);
    return 0;
}
~~~~~
</spoiler>





<spoiler summary="Putchar Non-recursive Dividing Implementation: 1980ms">
~~~~~
#include <iostream>

using namespace std;

inline void writeInt(int x)
{
    if (x < 0) putchar('-'), x = -x;
    int p = 1;
    for (int t = x / 10; t > 0; t /= 10)
        p *= 10;
    for (; p > 0; x %= p, p /= 10)
        putchar(x / p + '0');
}

int main()
{
    int q = 1e3;
    while (q--)
        for (int i = 0; i <= 1e4; ++i)
            writeInt(i);
    return 0;
}
~~~~~
</spoiler>





<spoiler summary="Putchar Non-recursive toString Implementation: 1934ms">
~~~~~
#include <iostream>

using namespace std;

char os[20];
inline void writeInt(int n)
{
    if (n < 0) putchar('-'), n = -n;
    int i=0;
    do os[i++] = n%10; while(n/=10);
    while (i--) putchar(os[i] + 48);
}

int main()
{
    int q = 1e3;
    while (q--)
        for (int i = 0; i <= 1e4; ++i)
            writeInt(i);
    return 0;
}
~~~~~
</spoiler>





<spoiler summary="Putchar Recursive Implementation: 1887ms">
~~~~~
#include <iostream>

using namespace std;

inline void writeRec(int n) {
    if (n > 9) writeRec(n / 10);
    putchar(char(n % 10 + '0'));
}

inline void writeInt(int x)
{
    if (x < 0) putchar('-'), x = -x;
    writeRec(x);
}

int main()
{
    int q = 1e3;
    while (q--)
        for (int i = 0; i <= 1e4; ++i)
            writeInt(i);
    return 0;
}
~~~~~
</spoiler>





<spoiler summary="Printf Implementation: 1216ms">
~~~~~
#include <cstdio>

using namespace std;

int main()
{
    int q = 1e3;
    while (q--)
        for (int i = 0; i <= 1e4; ++i)
            printf("%d", i);
    return 0;
}
~~~~~
</spoiler>





<spoiler summary="synchronized(on) Implementation: 873ms">
~~~~~
#include <iostream>

using namespace std;

int main()
{
    ios::sync_with_stdio(true),cin.tie(NULL),cout.tie(NULL);
    int q = 1e3;
    while (q--)
        for (int i = 0; i <= 1e4; ++i)
            cout << i;
    return 0;
}
~~~~~
</spoiler>





<spoiler summary="Normal Cout Implementation: 873ms">
~~~~~
#include <iostream>

using namespace std;

int main()
{
    int q = 1e3;
    while (q--)
        for (int i = 0; i <= 1e4; ++i)
            cout << i;
    return 0;
}
~~~~~
</spoiler>





<spoiler summary="synchronized(off) Cout Implementation: 857ms">
~~~~~
#include <iostream>

using namespace std;

int main()
{
    ios::sync_with_stdio(NULL),cin.tie(NULL),cout.tie(NULL);
    int q = 1e3;
    while (q--)
        for (int i = 0; i <= 1e4; ++i)
            cout << i;
    return 0;
}
~~~~~
</spoiler>





<spoiler summary="Unlocked-Putchar Non-recursive Dividing Implementation: 483ms">
~~~~~
#include <iostream>

using namespace std;

inline void writeInt(int x)
{
    if (x < 0) _putchar_nolock('-'), x = -x;
    int p = 1;
    for (int t = x / 10; t > 0; t /= 10)
        p *= 10;
    for (; p > 0; x %= p, p /= 10)
        _putchar_nolock(x / p + '0');
}

int main()
{
    int q = 1e3;
    while (q--)
        for (int i = 0; i <= 1e4; ++i)
            writeInt(i);
    return 0;
}
~~~~~
</spoiler>





<spoiler summary="Unlocked-Putchar Reverse Implementation: 467ms">
~~~~~
#include <iostream>

using namespace std;

#define pc _putchar_nolock
inline void writeInt(int n)
{
    if (n < 0) pc('-'), n = -n;
    if (!n) return (void)pc('0');
    int t = n, cnt = 0, rev = 0;
    while (!(t%10)) { cnt++; t /= 10;}
    do {rev=rev*10 + n%10;} while(n /= 10); 
    do {pc(rev % 10 + 48);} while(rev /= 10);
    while (cnt--) pc('0');
}

int main()
{
    int q = 1e3;
    while (q--)
        for (int i = 0; i <= 1e4; ++i)
            writeInt(i);
    return 0;
}
~~~~~
</spoiler>





<spoiler summary="Unlocked-Putchar Recursive Implementation: 358ms">
~~~~~
#include <iostream>

using namespace std;

inline void writeRec(int n) {
    if (n > 9) writeRec(n / 10);
    _putchar_nolock(char(n % 10 + '0'));
}

inline void writeInt(int x)
{
    if (x < 0) _putchar_nolock('-'), x = -x;
    writeRec(x);
}

int main()
{
    int q = 1e3;
    while (q--)
        for (int i = 0; i <= 1e4; ++i)
            writeInt(i);
    return 0;
}
~~~~~
</spoiler>





<spoiler summary="Unlocked-Putchar Non-recursive toString Implementation: 373ms">
~~~~~
#include <iostream>

using namespace std;

char os[20];
inline void writeInt(int n)
{
    if (n < 0) _putchar_nolock('-'), n = -n;
    int i=0;
    do os[i++] = n%10; while(n/=10);
    while (i--) _putchar_nolock(os[i] + 48);
}

int main()
{
    int q = 1e3;
    while (q--)
        for (int i = 0; i <= 1e4; ++i)
            writeInt(i);
    return 0;
}
~~~~~
</spoiler>





<spoiler summary="fwrite buffer Implementation: 311ms">
~~~~~
#include <iostream>

using namespace std;

static const int buf_len = (1 << 14);
static const int buf_max = (1 << 04);
static char buf_out[buf_len];
static char buf_num[buf_max];
static int buf_pos = 0;

inline void writeChar(int x) {
    if (buf_pos == buf_len) fwrite(buf_out, 1, buf_len, stdout), buf_pos = 0;
    buf_out[buf_pos++] = x;
}

inline void writeInt(int x, char end = 0) {
    if (x < 0) writeChar('-'), x = -x;
    int n = 0;
    do buf_num[n++] = x % 10 + '0'; while(x /= 10);
    while (n--) writeChar(buf_num[n]);
    if (end) writeChar(end);
}

struct Flusher{~Flusher(){if(buf_pos)fwrite(buf_out, 1, buf_pos, stdout),buf_pos=0;}}flusher;


int main()
{
    int q = 1e3;
    while (q--)
        for (int i = 0; i <= 1e4; ++i)
            writeInt(i);
    Flusher();
    return 0;
}
~~~~~
</spoiler>

</spoiler>














































<spoiler summary="Sort by GNU G++ 14 6.4.0">

<spoiler summary="Putchar Reverse Implementation: 1996ms">
~~~~~
#include <iostream>

using namespace std;

#define pc putchar
inline void writeInt(int n)
{
    if (n < 0) pc('-'), n = -n;
    if (!n) return (void)pc('0');
    int t = n, cnt = 0, rev = 0;
    while (!(t%10)) { cnt++; t /= 10;}
    do {rev=rev*10 + n%10;} while(n /= 10); 
    do {pc(rev % 10 + 48);} while(rev /= 10);
    while (cnt--) pc('0');
}

int main()
{
    int q = 1e3;
    while (q--)
        for (int i = 0; i <= 1e4; ++i)
            writeInt(i);
    return 0;
}
~~~~~
</spoiler>





<spoiler summary="Putchar Non-recursive Dividing Implementation: 1996ms">
~~~~~
#include <iostream>

using namespace std;

inline void writeInt(int x)
{
    if (x < 0) putchar('-'), x = -x;
    int p = 1;
    for (int t = x / 10; t > 0; t /= 10)
        p *= 10;
    for (; p > 0; x %= p, p /= 10)
        putchar(x / p + '0');
}

int main()
{
    int q = 1e3;
    while (q--)
        for (int i = 0; i <= 1e4; ++i)
            writeInt(i);
    return 0;
}
~~~~~
</spoiler>





<spoiler summary="Putchar Non-recursive toString Implementation: 1903ms">
~~~~~
#include <iostream>

using namespace std;

char os[20];
inline void writeInt(int n)
{
    if (n < 0) putchar('-'), n = -n;
    int i=0;
    do os[i++] = n%10; while(n/=10);
    while (i--) putchar(os[i] + 48);
}

int main()
{
    int q = 1e3;
    while (q--)
        for (int i = 0; i <= 1e4; ++i)
            writeInt(i);
    return 0;
}
~~~~~
</spoiler>





<spoiler summary="Putchar Recursive Implementation: 1871ms">
~~~~~
#include <iostream>

using namespace std;

inline void writeRec(int n) {
    if (n > 9) writeRec(n / 10);
    putchar(char(n % 10 + '0'));
}

inline void writeInt(int x)
{
    if (x < 0) putchar('-'), x = -x;
    writeRec(x);
}

int main()
{
    int q = 1e3;
    while (q--)
        for (int i = 0; i <= 1e4; ++i)
            writeInt(i);
    return 0;
}
~~~~~
</spoiler>





<spoiler summary="Printf Implementation: 1153ms">
~~~~~
#include <cstdio>

using namespace std;

int main()
{
    int q = 1e3;
    while (q--)
        for (int i = 0; i <= 1e4; ++i)
            printf("%d", i);
    return 0;
}
~~~~~
</spoiler>





<spoiler summary="synchronized(off) Cout Implementation: 920ms">
~~~~~
#include <iostream>

using namespace std;

int main()
{
    ios::sync_with_stdio(NULL),cin.tie(NULL),cout.tie(NULL);
    int q = 1e3;
    while (q--)
        for (int i = 0; i <= 1e4; ++i)
            cout << i;
    return 0;
}
~~~~~
</spoiler>





<spoiler summary="synchronized(on) Implementation: 888ms">
~~~~~
#include <iostream>

using namespace std;

int main()
{
    ios::sync_with_stdio(true),cin.tie(NULL),cout.tie(NULL);
    int q = 1e3;
    while (q--)
        for (int i = 0; i <= 1e4; ++i)
            cout << i;
    return 0;
}
~~~~~
</spoiler>





<spoiler summary="Normal Cout Implementation: 873ms">
~~~~~
#include <iostream>

using namespace std;

int main()
{
    int q = 1e3;
    while (q--)
        for (int i = 0; i <= 1e4; ++i)
            cout << i;
    return 0;
}
~~~~~
</spoiler>





<spoiler summary="Unlocked-Putchar Non-recursive Dividing Implementation: 452ms">
~~~~~
#include <iostream>

using namespace std;

inline void writeInt(int x)
{
    if (x < 0) _putchar_nolock('-'), x = -x;
    int p = 1;
    for (int t = x / 10; t > 0; t /= 10)
        p *= 10;
    for (; p > 0; x %= p, p /= 10)
        _putchar_nolock(x / p + '0');
}

int main()
{
    int q = 1e3;
    while (q--)
        for (int i = 0; i <= 1e4; ++i)
            writeInt(i);
    return 0;
}
~~~~~
</spoiler>





<spoiler summary="Unlocked-Putchar Reverse Implementation: 404ms">
~~~~~
#include <iostream>

using namespace std;

#define pc _putchar_nolock
inline void writeInt(int n)
{
    if (n < 0) pc('-'), n = -n;
    if (!n) return (void)pc('0');
    int t = n, cnt = 0, rev = 0;
    while (!(t%10)) { cnt++; t /= 10;}
    do {rev=rev*10 + n%10;} while(n /= 10); 
    do {pc(rev % 10 + 48);} while(rev /= 10);
    while (cnt--) pc('0');
}

int main()
{
    int q = 1e3;
    while (q--)
        for (int i = 0; i <= 1e4; ++i)
            writeInt(i);
    return 0;
}
~~~~~
</spoiler>





<spoiler summary="Unlocked-Putchar Non-recursive toString Implementation: 296ms">
~~~~~
#include <iostream>

using namespace std;

char os[20];
inline void writeInt(int n)
{
    if (n < 0) _putchar_nolock('-'), n = -n;
    int i=0;
    do os[i++] = n%10; while(n/=10);
    while (i--) _putchar_nolock(os[i] + 48);
}

int main()
{
    int q = 1e3;
    while (q--)
        for (int i = 0; i <= 1e4; ++i)
            writeInt(i);
    return 0;
}
~~~~~
</spoiler>





<spoiler summary="Unlocked-Putchar Recursive Implementation: 295ms">
~~~~~
#include <iostream>

using namespace std;

inline void writeRec(int n) {
    if (n > 9) writeRec(n / 10);
    _putchar_nolock(char(n % 10 + '0'));
}

inline void writeInt(int x)
{
    if (x < 0) _putchar_nolock('-'), x = -x;
    writeRec(x);
}

int main()
{
    int q = 1e3;
    while (q--)
        for (int i = 0; i <= 1e4; ++i)
            writeInt(i);
    return 0;
}
~~~~~
</spoiler>





<spoiler summary="fwrite buffer Implementation: 233ms">
~~~~~
#include <iostream>

using namespace std;

static const int buf_len = (1 << 14);
static const int buf_max = (1 << 04);
static char buf_out[buf_len];
static char buf_num[buf_max];
static int buf_pos = 0;

inline void writeChar(int x) {
    if (buf_pos == buf_len) fwrite(buf_out, 1, buf_len, stdout), buf_pos = 0;
    buf_out[buf_pos++] = x;
}

inline void writeInt(int x, char end = 0) {
    if (x < 0) writeChar('-'), x = -x;
    int n = 0;
    do buf_num[n++] = x % 10 + '0'; while(x /= 10);
    while (n--) writeChar(buf_num[n]);
    if (end) writeChar(end);
}

struct Flusher{~Flusher(){if(buf_pos)fwrite(buf_out, 1, buf_pos, stdout),buf_pos=0;}}flusher;


int main()
{
    int q = 1e3;
    while (q--)
        for (int i = 0; i <= 1e4; ++i)
            writeInt(i);
    Flusher();
    return 0;
}
~~~~~
</spoiler>

</spoiler>














































<spoiler summary="Sort by GNU G++ 11 5.1.0">

<spoiler summary="synchronized(on) Implementation: 2698ms">
~~~~~
#include <iostream>

using namespace std;

int main()
{
    ios::sync_with_stdio(true),cin.tie(NULL),cout.tie(NULL);
    int q = 1e3;
    while (q--)
        for (int i = 0; i <= 1e4; ++i)
            cout << i;
    return 0;
}
~~~~~
</spoiler>





<spoiler summary="Normal Cout Implementation: 2698ms">
~~~~~
#include <iostream>

using namespace std;

int main()
{
    int q = 1e3;
    while (q--)
        for (int i = 0; i <= 1e4; ++i)
            cout << i;
    return 0;
}
~~~~~
</spoiler>





<spoiler summary="synchronized(off) Cout Implementation: 2620ms">
~~~~~
#include <iostream>

using namespace std;

int main()
{
    ios::sync_with_stdio(NULL),cin.tie(NULL),cout.tie(NULL);
    int q = 1e3;
    while (q--)
        for (int i = 0; i <= 1e4; ++i)
            cout << i;
    return 0;
}
~~~~~
</spoiler>





<spoiler summary="Printf Implementation: 1403ms">
~~~~~
#include <cstdio>

using namespace std;

int main()
{
    int q = 1e3;
    while (q--)
        for (int i = 0; i <= 1e4; ++i)
            printf("%d", i);
    return 0;
}
~~~~~
</spoiler>





<spoiler summary="Putchar Non-recursive Dividing Implementation: 405ms">
~~~~~
#include <iostream>

using namespace std;

inline void writeInt(int x)
{
    if (x < 0) putchar('-'), x = -x;
    int p = 1;
    for (int t = x / 10; t > 0; t /= 10)
        p *= 10;
    for (; p > 0; x %= p, p /= 10)
        putchar(x / p + '0');
}

int main()
{
    int q = 1e3;
    while (q--)
        for (int i = 0; i <= 1e4; ++i)
            writeInt(i);
    return 0;
}
~~~~~
</spoiler>





<spoiler summary="Putchar Reverse Implementation: 343ms">
~~~~~
#include <iostream>

using namespace std;

#define pc putchar
inline void writeInt(int n)
{
    if (n < 0) pc('-'), n = -n;
    if (!n) return (void)pc('0');
    int t = n, cnt = 0, rev = 0;
    while (!(t%10)) { cnt++; t /= 10;}
    do {rev=rev*10 + n%10;} while(n /= 10); 
    do {pc(rev % 10 + 48);} while(rev /= 10);
    while (cnt--) pc('0');
}

int main()
{
    int q = 1e3;
    while (q--)
        for (int i = 0; i <= 1e4; ++i)
            writeInt(i);
    return 0;
}
~~~~~
</spoiler>





<spoiler summary="fwrite buffer Implementation: 265ms">
~~~~~
#include <iostream>

using namespace std;

static const int buf_len = (1 << 14);
static const int buf_max = (1 << 04);
static char buf_out[buf_len];
static char buf_num[buf_max];
static int buf_pos = 0;

inline void writeChar(int x) {
    if (buf_pos == buf_len) fwrite(buf_out, 1, buf_len, stdout), buf_pos = 0;
    buf_out[buf_pos++] = x;
}

inline void writeInt(int x, char end = 0) {
    if (x < 0) writeChar('-'), x = -x;
    int n = 0;
    do buf_num[n++] = x % 10 + '0'; while(x /= 10);
    while (n--) writeChar(buf_num[n]);
    if (end) writeChar(end);
}

struct Flusher{~Flusher(){if(buf_pos)fwrite(buf_out, 1, buf_pos, stdout),buf_pos=0;}}flusher;


int main()
{
    int q = 1e3;
    while (q--)
        for (int i = 0; i <= 1e4; ++i)
            writeInt(i);
    Flusher();
    return 0;
}
~~~~~
</spoiler>





<spoiler summary="Putchar Non-recursive toString Implementation: 249ms">
~~~~~
#include <iostream>

using namespace std;

char os[20];
inline void writeInt(int n)
{
    if (n < 0) putchar('-'), n = -n;
    int i=0;
    do os[i++] = n%10; while(n/=10);
    while (i--) putchar(os[i] + 48);
}

int main()
{
    int q = 1e3;
    while (q--)
        for (int i = 0; i <= 1e4; ++i)
            writeInt(i);
    return 0;
}
~~~~~
</spoiler>





<spoiler summary="Putchar Recursive Implementation: 233ms">
~~~~~
#include <iostream>

using namespace std;

inline void writeRec(int n) {
    if (n > 9) writeRec(n / 10);
    putchar(char(n % 10 + '0'));
}

inline void writeInt(int x)
{
    if (x < 0) putchar('-'), x = -x;
    writeRec(x);
}

int main()
{
    int q = 1e3;
    while (q--)
        for (int i = 0; i <= 1e4; ++i)
            writeInt(i);
    return 0;
}
~~~~~
</spoiler>

</spoiler>





















































































































































































































**Time to write first 10.000.000 non-positive numbers**

_(base on [Codeforces Custom Test](https://codeforces.com/problemset/customtest) // GNU G++ 17 7.3.0 // GNU G++ 14 6.4.0 // GNU G++ 11 5.1.0)_

<spoiler summary="Sort by GNU G++ 17 7.3.0">

<spoiler summary="Putchar Non-recursive toString Implementation: 3946ms">
~~~~~
#include <iostream>

using namespace std;

char os[20];
inline void writeInt(int n)
{
    if (n < 0) putchar('-'), n = -n;
    int i=0;
    do os[i++] = n%10; while(n/=10);
    while (i--) putchar(os[i] + 48);
}

int main()
{
    int q = 1e7;
    while (q--) writeInt(-q);
    return 0;
}
~~~~~
</spoiler>





<spoiler summary="Putchar Reverse Implementation: 3930ms">
~~~~~
#include <iostream>

using namespace std;

#define pc putchar
inline void writeInt(int n)
{
    if (n < 0) pc('-'), n = -n;
    if (!n) return (void)pc('0');
    int t = n, cnt = 0, rev = 0;
    while (!(t%10)) { cnt++; t /= 10;}
    do {rev=rev*10 + n%10;} while(n /= 10); 
    do {pc(rev % 10 + 48);} while(rev /= 10);
    while (cnt--) pc('0');
}

int main()
{
    int q = 1e7;
    while (q--) writeInt(-q);
    return 0;
}
~~~~~
</spoiler>





<spoiler summary="Putchar Recursive Implementation: 3915ms">
~~~~~
#include <iostream>

using namespace std;

inline void writeRec(int n) {
    if (n > 9) writeRec(n / 10);
    putchar(char(n % 10 + '0'));
}

inline void writeInt(int x)
{
    if (x < 0) putchar('-');
    writeRec(abs(x));
}

int main()
{
    int q = 1e7;
    while (q--) writeInt(-q);
    return 0;
}
~~~~~
</spoiler>





<spoiler summary="Putchar Non-recursive Dividing Implementation: 3883ms">
~~~~~
#include <iostream>

using namespace std;

inline void writeInt(int x)
{
    if (x < 0) putchar('-'), x = -x;
    int p = 1;
    for (int t = x / 10; t > 0; t /= 10)
        p *= 10;
    for (; p > 0; x %= p, p /= 10) putchar(x / p + '0');
}

int main()
{
    int q = 1e7;
    while (q--) writeInt(-q);
    return 0;
}
~~~~~
</spoiler>




<spoiler summary="Printf Implementation: 1808ms">
~~~~~
#include <cstdio>

using namespace std;

int main()
{
    int q = 1e7;
    while (q--) printf("%d", -q);
    return 0;
}
~~~~~
</spoiler>





<spoiler summary="synchronized(off) Cout Implementation: 1481ms">
~~~~~
#include <iostream>

using namespace std;

int main()
{
    ios::sync_with_stdio(NULL),cin.tie(NULL),cout.tie(NULL);
    int q = 1e7;
    while (q--) cout << -q;
    return 0;
}
~~~~~
</spoiler>





<spoiler summary="synchronized(true) Cout Implementation: 1092ms">
~~~~~
#include <iostream>

using namespace std;

int main()
{
    ios::sync_with_stdio(true),cin.tie(NULL),cout.tie(NULL);
    int q = 1e7;
    while (q--) cout << -q;
    return 0;
}
~~~~~
</spoiler>





<spoiler summary="Normal Cout Implementation: 1092ms">
~~~~~
#include <iostream>

using namespace std;

int main()
{
    int q = 1e7;
    while (q--) cout << -q;
    return 0;
}
~~~~~
</spoiler>





<spoiler summary="Unlocked-Putchar Non-recursive Dividing Implementation: 1045ms">
~~~~~
#include <iostream>

using namespace std;

inline void writeInt(int x)
{
    if (x < 0) _putchar_nolock('-'), x = -x;
    int p = 1;
    for (int t = x / 10; t > 0; t /= 10)
        p *= 10;
    for (; p > 0; x %= p, p /= 10)
        _putchar_nolock(x / p + '0');
}

int main()
{
    int q = 1e7;
    while (q--) writeInt(-q);
    return 0;
}
~~~~~
</spoiler>





<spoiler summary="Unlocked-Putchar Reverse Implementation: 857ms">
~~~~~
#include <iostream>

using namespace std;

#define pc _putchar_nolock
inline void writeInt(int n)
{
    if (n < 0) pc('-'), n = -n;
    if (!n) return (void)pc('0');
    int t = n, cnt = 0, rev = 0;
    while (!(t%10)) { cnt++; t /= 10;}
    do {rev=rev*10 + n%10;} while(n /= 10); 
    do {pc(rev % 10 + 48);} while(rev /= 10);
    while (cnt--) pc('0');
}

int main()
{
    int q = 1e7;
    while (q--) writeInt(-q);
    return 0;
}
~~~~~
</spoiler>





<spoiler summary="Unlocked-Putchar Non-recursive toString Implementation: 795ms">
~~~~~
#include <iostream>

using namespace std;

char os[20];
inline void writeInt(int n)
{
    if (n < 0) _putchar_nolock('-'), n = -n;
    int i=0;
    do os[i++] = n%10; while(n/=10);
    while (i--) _putchar_nolock(os[i] + 48);
}

int main()
{
    int q = 1e7;
    while (q--) writeInt(-q);
    return 0;
}
~~~~~
</spoiler>





<spoiler summary="Unlocked-Putchar Recursive Implementation: 779ms">
~~~~~
#include <iostream>

using namespace std;

inline void writeRec(int n) {
    if (n > 9) writeRec(n / 10);
    _putchar_nolock(char(n % 10 + '0'));
}

inline void writeInt(int x)
{
    if (x < 0) _putchar_nolock('-'), x = -x;
    writeRec(x);
}

int main()
{
    int q = 1e7;
    while (q--) writeInt(-q);
    return 0;
}
~~~~~
</spoiler>





<spoiler summary="fwrite buffer Implementation: 561ms">
~~~~~
#include <iostream>

using namespace std;

static const int buf_len = (1 << 14);
static const int buf_max = (1 << 04);
static char buf_out[buf_len];
static char buf_num[buf_max];
static int buf_pos = 0;

inline void writeChar(int x) {
    if (buf_pos == buf_len) fwrite(buf_out, 1, buf_len, stdout), buf_pos = 0;
    buf_out[buf_pos++] = x;
}

inline void writeInt(int x, char end = 0) {
    if (x < 0) writeChar('-'), x = -x;
    int n = 0;
    do buf_num[n++] = x % 10 + '0'; while(x /= 10);
    while (n--) writeChar(buf_num[n]);
    if (end) writeChar(end);
}

struct Flusher{~Flusher(){if(buf_pos)fwrite(buf_out, 1, buf_pos, stdout),buf_pos=0;}}flusher;

int main()
{
    int q = 1e7;
    while (q--) writeInt(-q); Flusher();
    return 0;
}
~~~~~
</spoiler>

</spoiler>













































<spoiler summary="Sort by GNU G++ 14 6.4.0">

<spoiler summary="Putchar Reverse Implementation: 3899ms">
~~~~~
#include <iostream>

using namespace std;

#define pc putchar
inline void writeInt(int n)
{
    if (n < 0) pc('-'), n = -n;
    if (!n) return (void)pc('0');
    int t = n, cnt = 0, rev = 0;
    while (!(t%10)) { cnt++; t /= 10;}
    do {rev=rev*10 + n%10;} while(n /= 10); 
    do {pc(rev % 10 + 48);} while(rev /= 10);
    while (cnt--) pc('0');
}

int main()
{
    int q = 1e7;
    while (q--) writeInt(-q);
    return 0;
}
~~~~~
</spoiler>





<spoiler summary="Putchar Recursive Implementation: 3899ms">
~~~~~
#include <iostream>

using namespace std;

inline void writeRec(int n) {
    if (n > 9) writeRec(n / 10);
    putchar(char(n % 10 + '0'));
}

inline void writeInt(int x)
{
    if (x < 0) putchar('-');
    writeRec(abs(x));
}

int main()
{
    int q = 1e7;
    while (q--) writeInt(-q);
    return 0;
}
~~~~~
</spoiler>





<spoiler summary="Putchar Non-recursive Dividing Implementation: 3883ms">
~~~~~
#include <iostream>

using namespace std;

inline void writeInt(int x)
{
    if (x < 0) putchar('-'), x = -x;
    int p = 1;
    for (int t = x / 10; t > 0; t /= 10)
        p *= 10;
    for (; p > 0; x %= p, p /= 10) putchar(x / p + '0');
}

int main()
{
    int q = 1e7;
    while (q--) writeInt(-q);
    return 0;
}
~~~~~
</spoiler>




<spoiler summary="Putchar Non-recursive toString Implementation: 3860ms">
~~~~~
#include <iostream>

using namespace std;

char os[20];
inline void writeInt(int n)
{
    if (n < 0) putchar('-'), n = -n;
    int i=0;
    do os[i++] = n%10; while(n/=10);
    while (i--) putchar(os[i] + 48);
}

int main()
{
    int q = 1e7;
    while (q--) writeInt(-q);
    return 0;
}
~~~~~
</spoiler>




<spoiler summary="Printf Implementation: 1762ms">
~~~~~
#include <cstdio>

using namespace std;

int main()
{
    int q = 1e7;
    while (q--) printf("%d", -q);
    return 0;
}
~~~~~
</spoiler>





<spoiler summary="synchronized(off) Cout Implementation: 1512ms">
~~~~~
#include <iostream>

using namespace std;

int main()
{
    ios::sync_with_stdio(NULL),cin.tie(NULL),cout.tie(NULL);
    int q = 1e7;
    while (q--) cout << -q;
    return 0;
}
~~~~~
</spoiler>





<spoiler summary="Normal Cout Implementation: 1153ms">
~~~~~
#include <iostream>

using namespace std;

int main()
{
    int q = 1e7;
    while (q--) cout << -q;
    return 0;
}
~~~~~
</spoiler>





<spoiler summary="synchronized(true) Cout Implementation: 1092ms">
~~~~~
#include <iostream>

using namespace std;

int main()
{
    ios::sync_with_stdio(true),cin.tie(NULL),cout.tie(NULL);
    int q = 1e7;
    while (q--) cout << -q;
    return 0;
}
~~~~~
</spoiler>





<spoiler summary="Unlocked-Putchar Non-recursive Dividing Implementation: 951ms">
~~~~~
#include <iostream>

using namespace std;

inline void writeInt(int x)
{
    if (x < 0) _putchar_nolock('-'), x = -x;
    int p = 1;
    for (int t = x / 10; t > 0; t /= 10)
        p *= 10;
    for (; p > 0; x %= p, p /= 10)
        _putchar_nolock(x / p + '0');
}

int main()
{
    int q = 1e7;
    while (q--) writeInt(-q);
    return 0;
}
~~~~~
</spoiler>





<spoiler summary="Unlocked-Putchar Reverse Implementation: 732ms">
~~~~~
#include <iostream>

using namespace std;

#define pc _putchar_nolock
inline void writeInt(int n)
{
    if (n < 0) pc('-'), n = -n;
    if (!n) return (void)pc('0');
    int t = n, cnt = 0, rev = 0;
    while (!(t%10)) { cnt++; t /= 10;}
    do {rev=rev*10 + n%10;} while(n /= 10); 
    do {pc(rev % 10 + 48);} while(rev /= 10);
    while (cnt--) pc('0');
}

int main()
{
    int q = 1e7;
    while (q--) writeInt(-q);
    return 0;
}
~~~~~
</spoiler>





<spoiler summary="Unlocked-Putchar Recursive Implementation: 655ms">
~~~~~
#include <iostream>

using namespace std;

inline void writeRec(int n) {
    if (n > 9) writeRec(n / 10);
    _putchar_nolock(char(n % 10 + '0'));
}

inline void writeInt(int x)
{
    if (x < 0) _putchar_nolock('-'), x = -x;
    writeRec(x);
}

int main()
{
    int q = 1e7;
    while (q--) writeInt(-q);
    return 0;
}
~~~~~
</spoiler>





<spoiler summary="Unlocked-Putchar Non-recursive toString Implementation: 638ms">
~~~~~
#include <iostream>

using namespace std;

char os[20];
inline void writeInt(int n)
{
    if (n < 0) _putchar_nolock('-'), n = -n;
    int i=0;
    do os[i++] = n%10; while(n/=10);
    while (i--) _putchar_nolock(os[i] + 48);
}

int main()
{
    int q = 1e7;
    while (q--) writeInt(-q);
    return 0;
}
~~~~~
</spoiler>





<spoiler summary="fwrite buffer Implementation: 529ms">
~~~~~
#include <iostream>

using namespace std;

static const int buf_len = (1 << 14);
static const int buf_max = (1 << 04);
static char buf_out[buf_len];
static char buf_num[buf_max];
static int buf_pos = 0;

inline void writeChar(int x) {
    if (buf_pos == buf_len) fwrite(buf_out, 1, buf_len, stdout), buf_pos = 0;
    buf_out[buf_pos++] = x;
}

inline void writeInt(int x, char end = 0) {
    if (x < 0) writeChar('-'), x = -x;
    int n = 0;
    do buf_num[n++] = x % 10 + '0'; while(x /= 10);
    while (n--) writeChar(buf_num[n]);
    if (end) writeChar(end);
}

struct Flusher{~Flusher(){if(buf_pos)fwrite(buf_out, 1, buf_pos, stdout),buf_pos=0;}}flusher;

int main()
{
    int q = 1e7;
    while (q--) writeInt(-q); Flusher();
    return 0;
}
~~~~~
</spoiler>

</spoiler>













































<spoiler summary="Sort by GNU G++ 11 5.1.0">

<spoiler summary="synchronized(true) Cout Implementation: 2901ms">
~~~~~
#include <iostream>

using namespace std;

int main()
{
    ios::sync_with_stdio(true),cin.tie(NULL),cout.tie(NULL);
    int q = 1e7;
    while (q--) cout << -q;
    return 0;
}
~~~~~
</spoiler>





<spoiler summary="Normal Cout Implementation: 2901ms">
~~~~~
#include <iostream>

using namespace std;

int main()
{
    int q = 1e7;
    while (q--) cout << -q;
    return 0;
}
~~~~~
</spoiler>





<spoiler summary="synchronized(off) Cout Implementation: 2885ms">
~~~~~
#include <iostream>

using namespace std;

int main()
{
    ios::sync_with_stdio(NULL),cin.tie(NULL),cout.tie(NULL);
    int q = 1e7;
    while (q--) cout << -q;
    return 0;
}
~~~~~
</spoiler>




<spoiler summary="Printf Implementation: 1950ms">
~~~~~
#include <cstdio>

using namespace std;

int main()
{
    int q = 1e7;
    while (q--) printf("%d", -q);
    return 0;
}
~~~~~
</spoiler>





<spoiler summary="Putchar Non-recursive Dividing Implementation: 810ms">
~~~~~
#include <iostream>

using namespace std;

inline void writeInt(int x)
{
    if (x < 0) putchar('-'), x = -x;
    int p = 1;
    for (int t = x / 10; t > 0; t /= 10)
        p *= 10;
    for (; p > 0; x %= p, p /= 10) putchar(x / p + '0');
}

int main()
{
    int q = 1e7;
    while (q--) writeInt(-q);
    return 0;
}
~~~~~
</spoiler>





<spoiler summary="Putchar Reverse Implementation: 624ms">
~~~~~
#include <iostream>

using namespace std;

#define pc putchar
inline void writeInt(int n)
{
    if (n < 0) pc('-'), n = -n;
    if (!n) return (void)pc('0');
    int t = n, cnt = 0, rev = 0;
    while (!(t%10)) { cnt++; t /= 10;}
    do {rev=rev*10 + n%10;} while(n /= 10); 
    do {pc(rev % 10 + 48);} while(rev /= 10);
    while (cnt--) pc('0');
}

int main()
{
    int q = 1e7;
    while (q--) writeInt(-q);
    return 0;
}
~~~~~
</spoiler>





<spoiler summary="fwrite buffer Implementation: 483ms">
~~~~~
#include <iostream>

using namespace std;

static const int buf_len = (1 << 14);
static const int buf_max = (1 << 04);
static char buf_out[buf_len];
static char buf_num[buf_max];
static int buf_pos = 0;

inline void writeChar(int x) {
    if (buf_pos == buf_len) fwrite(buf_out, 1, buf_len, stdout), buf_pos = 0;
    buf_out[buf_pos++] = x;
}

inline void writeInt(int x, char end = 0) {
    if (x < 0) writeChar('-'), x = -x;
    int n = 0;
    do buf_num[n++] = x % 10 + '0'; while(x /= 10);
    while (n--) writeChar(buf_num[n]);
    if (end) writeChar(end);
}

struct Flusher{~Flusher(){if(buf_pos)fwrite(buf_out, 1, buf_pos, stdout),buf_pos=0;}}flusher;

int main()
{
    int q = 1e7;
    while (q--) writeInt(-q); Flusher();
    return 0;
}
~~~~~
</spoiler>





<spoiler summary="Putchar Non-recursive toString Implementation: 483ms">
~~~~~
#include <iostream>

using namespace std;

char os[20];
inline void writeInt(int n)
{
    if (n < 0) putchar('-'), n = -n;
    int i=0;
    do os[i++] = n%10; while(n/=10);
    while (i--) putchar(os[i] + 48);
}

int main()
{
    int q = 1e7;
    while (q--) writeInt(-q);
    return 0;
}
~~~~~
</spoiler>





<spoiler summary="Putchar Recursive Implementation: 452ms">
~~~~~
#include <iostream>

using namespace std;

inline void writeRec(int n) {
    if (n > 9) writeRec(n / 10);
    putchar(char(n % 10 + '0'));
}

inline void writeInt(int x)
{
    if (x < 0) putchar('-');
    writeRec(abs(x));
}

int main()
{
    int q = 1e7;
    while (q--) writeInt(-q);
    return 0;
}
~~~~~
</spoiler>

</spoiler>





















































































































































































































**Single Line Template** 

<spoiler summary="Putchar Non-recursive toString Implementation">
~~~~~
char os[20];
inline void writeInt(int n){if(n<0)putchar('-'),n=-n;int i=0;do{os[i++]=n%10;}while(n/=10);while(i--)putchar(os[i]+48);}
~~~~~
</spoiler>





<spoiler summary="Putchar Non-recursive Dividing Implementation">
~~~~~
inline void writeInt(int x){if(x<0)putchar('-'),x=-x;int p=1;for(int t=x/10;t>0;t/=10)p*=10;for(;p>0;x%=p,p/=10)putchar(x/p+'0');}
~~~~~
</spoiler>





<spoiler summary="Putchar Reverse Implementation">
~~~~~
#define pc putchar
inline void writeInt(int n){if(n<0)pc('-'),n=-n;if(!n)return(void)pc('0');int t=n,cnt=0,rev=0;while(!(t%10)){cnt++;t/=10;}do{rev=rev*10+n%10;}while(n/=10);do{pc(rev%10+48);}while(rev/=10);while(cnt--)pc('0');}
~~~~~
</spoiler>





<spoiler summary="Putchar Recursive Implementation">
~~~~~
inline void writeRec(int n){if(n>9)writeRec(n/10);putchar(char(n%10+'0'));}
inline void writeInt(int x){if(x<0)putchar('-');writeRec(abs(x));}
~~~~~
</spoiler>





<spoiler summary="Unlocked-Putchar Non-recursive toString Implementation">
~~~~~
char os[20];
inline void writeInt(int n){if(n<0)_putchar_nolock('-'),n=-n;int i=0;do{os[i++]=n%10;}while(n/=10);while(i--)_putchar_nolock(os[i]+48);}
~~~~~
</spoiler>





<spoiler summary="Unlocked-Putchar Non-recursive Dividing Implementation">
~~~~~
inline void writeInt(int x){if(x<0)_putchar_nolock('-'),x=-x;int p=1;for(int t=x/10;t>0;t/=10)p*=10;for(;p>0;x%=p,p/=10)_putchar_nolock(x/p+'0');}
~~~~~
</spoiler>





<spoiler summary="Unlocked-Putchar Reverse Implementation">
~~~~~
#define pc _putchar_nolock
inline void writeInt(int n){if(n<0)pc('-'),n=-n;if(!n)return(void)pc('0');int t=n,cnt=0,rev=0;while(!(t%10)){cnt++;t/=10;}do{rev=rev*10+n%10;}while(n/=10);do{pc(rev%10+48);}while(rev/=10);while(cnt--)pc('0');}
~~~~~
</spoiler>





<spoiler summary="Unlocked-Putchar Recursive Implementation">
~~~~~
inline void writeRec(int n){if(n>9)writeRec(n/10);_putchar_nolock(char(n%10+'0'));}
inline void writeInt(int x){if(x<0)_putchar_nolock('-');writeRec(abs(x));}
~~~~~
</spoiler>




<spoiler summary="Printf Implementation">
~~~~~
printf("%d", x);
~~~~~
</spoiler>





<spoiler summary="synchronized(off) Implementation">
~~~~~
ios::sync_with_stdio(NULL),cin.tie(NULL),cout.tie(NULL);
~~~~~
</spoiler>





<spoiler summary="synchronized(true) Implementation">
~~~~~
ios::sync_with_stdio(true),cin.tie(NULL),cout.tie(NULL);
~~~~~
</spoiler>





<spoiler summary="Cout Implementation">
~~~~~
cout << x;
~~~~~
</spoiler>





<spoiler summary="fwrite buffer Implementation">
~~~~~
static const int buf_len = (1 << 14), buf_max = (1 << 04);
static char buf_out[buf_len], buf_num[buf_max];
static int buf_pos = 0;

inline void writeChar(int x){if(buf_pos==buf_len)fwrite(buf_out,1,buf_len,stdout),buf_pos=0;buf_out[buf_pos++]=x;}
inline void writeInt(int x,char end=0){if(x<0)writeChar('-'),x=-x;int n=0;do{buf_num[n++]=x%10+'0';}while(x/=10);while(n--)writeChar(buf_num[n]);if(end)writeChar(end);}
struct Flusher{~Flusher(){if(buf_pos)fwrite(buf_out, 1, buf_pos, stdout),buf_pos=0;}}flusher;
~~~~~
</spoiler>





















































































































































































































----------
**About:**
---------- 

- _[putchar()](http://www.cplusplus.com/reference/cstdio/putchar/)_
- _[putchar_unlocked()](https://www.mkssoftware.com/docs/man3/putchar_unlocked.3.asp)_
- _[putchar_nolock()](https://docs.microsoft.com/en-us/cpp/c-runtime-library/reference/putchar-nolock-putwchar-nolock?view=vs-2019)_
- _[printf()](http://www.cplusplus.com/reference/cstdio/printf/)_
- _[sync_with_stdio()](http://www.cplusplus.com/reference/ios/ios_base/sync_with_stdio/)_
- _[cin.tie(), cout.tie()](http://www.cplusplus.com/reference/ios/ios/tie/)_
- _[cout <<](http://www.cplusplus.com/reference/iostream/cout/)_
- _[fwrite](http://www.cplusplus.com/reference/cstdio/fwrite/)_





----------
**Similiar Topic:**
---------- 

- _[C++ Input Implementations ///// Are there ways to perform faster ?](https://codeforces.com/blog/entry/74659)_
- [Fast IO c++](https://codeforces.com/blog/entry/8080)
- [Fast I/O Code Optimizer](https://codeforces.com/blog/entry/65784)
- [Yet again on C++ input/output](https://codeforces.com/blog/entry/5217)
- [How to take fast I/O in C++?](https://codeforces.com/blog/entry/21562)
- [Fast and furious C++ I/O](https://codeforces.com/blog/entry/45835)
- [Best form of C++ I/O?](https://codeforces.com/blog/entry/6251)
- [What is the fastest way to take I/O in c++?](https://codeforces.com/blog/entry/70121)
- [Fast I/O using fread, fwrite](https://codeforces.com/blog/entry/11812)
- [Speed of Input/Output of various languages and method on Codeforces](https://codeforces.com/blog/entry/51544)
- [Speed up cin & cout in C++](https://codeforces.com/blog/entry/10297)




----------
**Planning:**
---------- 

- _Test about random 10.000.000 big numbers_
- _Test with Microsoft Visual C++ 2010_
- _Test with Microsoft Visual C++ 2017_
- _More implementations (Actually the post is about Faster and Faster Short Output Implementation but I will add some for speed comparing)_
- _New output types (long long, double, string)_
