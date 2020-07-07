# 0012_IntegertoRoman
## 想法
按照題目的意思做了各種 if-else & switch statement 的判斷
## 作法
Runtime: 16 ms (52.95%)
Memory Usage: 6.1 MB (61.26%)
```C++
class Solution {
public:
    string intToRoman(int num) {
        string s = "";
        int t=0;
        for (int i = 0; i < 4 && num != 0; ++i ) {
            int t = num % 10;
            num /= 10;
            if (t == 9) {
                switch(i) {
                    case 0:
                        s = "IX" + s;
                        break;
                    case 1:
                        s = "XC" + s;
                        break;
                    case 2:
                        s = "CM" + s;
                        break;
                        
                }
            }
            else if (t == 4) {
                switch(i) {
                    case 0:
                        s = "IV" + s;
                        break;
                    case 1:
                        s = "XL" + s;
                        break;
                    case 2:
                        s = "CD" + s;
                        break;
                }
            }
            else if (t >= 5){
                string ts = "";
                switch(i) {
                    case 0:
                        ts = "V";
                        break;
                    case 1:
                        ts = "L";
                        break;
                    case 2:
                        ts = "D";
                        break;
                }
                for (int j = t-5; j > 0; --j) {
                    switch(i) {
                        case 0:
                            ts += "I";
                            break;
                        case 1:
                            ts += "X";
                            break;
                        case 2:
                            ts += "C";
                            break;
                    }
                }
                s = ts + s;
            }
            else if (t >= 1){
                for (int j = t; j > 0; --j) {
                    switch(i) {
                        case 0:
                            s = "I" + s;
                            break;
                        case 1:
                            s = "X" + s;
                            break;
                        case 2:
                            s = "C" + s;
                            break;
                        case 3:
                            s = "M" + s;
                            break;
                    }
                }
            }
        }
        return s;
    }
};
```
