# lapply and sapply

Each of the *apply functions will SPLIT up some data into smaller pieces, APPLY afunction to each piece, then COMBINE the results.

We will start with data stored in a variable called flags. We see what is inside it.
```
> dim(flags)
[1] 194  30

> class(flags)
[1] "data.frame"

> head(flags)
            name landmass zone area population language religion bars stripes colours red
1    Afghanistan        5    1  648         16       10        2    0       3       5   1
2        Albania        3    1   29          3        6        6    0       0       3   1
3        Algeria        4    1 2388         20        8        2    2       0       3   1
4 American-Samoa        6    3    0          0        1        1    0       0       5   1
5        Andorra        3    1    0          0        6        0    3       0       3   1
6         Angola        4    2 1247          7       10        5    0       2       3   1
  green blue gold white black orange mainhue circles crosses saltires quarters sunstars
1     1    0    1     1     1      0   green       0       0        0        0        1
2     0    0    1     0     1      0     red       0       0        0        0        1
3     1    0    0     1     0      0   green       0       0        0        0        1
4     0    1    1     1     0      1    blue       0       0        0        0        0
5     0    1    1     0     0      0    gold       0       0        0        0        0
6     0    0    1     0     1      0     red       0       0        0        0        1
  crescent triangle icon animate text topleft botright
1        0        0    1       0    0   black    green
2        0        0    0       1    0     red      red
3        1        0    0       0    0   green    white
4        0        1    1       1    0    blue      red
5        0        0    0       0    0    blue      red
6        0        0    1       0    0     red    black
```

## as.list()
The lapply() function takes a list as input, applies a function to each element of the list, then returns a list of the same length as the original one. Remember that a Dataframe is a list of vectors. To see it like that, you can use the as.list() function.
```
> as.list(flags))
Error: unexpected ')' in "as.list(flags))"
> as.list(flags)
$name
  [1] Afghanistan              Albania                  Algeria                 
  [4] American-Samoa           Andorra                  Angola                  
  [7] Anguilla                 Antigua-Barbuda          Argentina               
 [10] Argentine                Australia                Austria                 
 [13] Bahamas                  Bahrain                  Bangladesh              
 [16] Barbados                 Belgium                  Belize                  
 [19] Benin                    Bermuda                  Bhutan                  
 [22] Bolivia                  Botswana                 Brazil                  
 [25] British-Virgin-Isles     Brunei                   Bulgaria                
 [28] Burkina                  Burma                    Burundi                 
 [31] Cameroon                 Canada                   Cape-Verde-Islands      
 [34] Cayman-Islands           Central-African-Republic Chad                    
 [37] Chile                    China                    Colombia                
 [40] Comorro-Islands          Congo                    Cook-Islands            
 [43] Costa-Rica               Cuba                     Cyprus                  
 [46] Czechoslovakia           Denmark                  Djibouti                
 [49] Dominica                 Dominican-Republic       Ecuador                 
 [52] Egypt                    El-Salvador              Equatorial-Guinea       
 [55] Ethiopia                 Faeroes                  Falklands-Malvinas      
 [58] Fiji                     Finland                  France                  
 [61] French-Guiana            French-Polynesia         Gabon                   
 [64] Gambia                   Germany-DDR              Germany-FRG             
 [67] Ghana                    Gibraltar                Greece                  
 [70] Greenland                Grenada                  Guam                    
 [73] Guatemala                Guinea                   Guinea-Bissau           
 [76] Guyana                   Haiti                    Honduras                
 [79] Hong-Kong                Hungary                  Iceland                 
 [82] India                    Indonesia                Iran                    
 [85] Iraq                     Ireland                  Israel                  
 [88] Italy                    Ivory-Coast              Jamaica                 
 [91] Japan                    Jordan                   Kampuchea               
 [94] Kenya                    Kiribati                 Kuwait                  
 [97] Laos                     Lebanon                  Lesotho                 
[100] Liberia                  Libya                    Liechtenstein           
[103] Luxembourg               Malagasy                 Malawi                  
[106] Malaysia                 Maldive-Islands          Mali                    
[109] Malta                    Marianas                 Mauritania              
[112] Mauritius                Mexico                   Micronesia              
[115] Monaco                   Mongolia                 Montserrat              
[118] Morocco                  Mozambique               Nauru                   
[121] Nepal                    Netherlands              Netherlands-Antilles    
[124] New-Zealand              Nicaragua                Niger                   
[127] Nigeria                  Niue                     North-Korea             
[130] North-Yemen              Norway                   Oman                    
[133] Pakistan                 Panama                   Papua-New-Guinea        
[136] Parguay                  Peru                     Philippines             
[139] Poland                   Portugal                 Puerto-Rico             
[142] Qatar                    Romania                  Rwanda                  
[145] San-Marino               Sao-Tome                 Saudi-Arabia            
[148] Senegal                  Seychelles               Sierra-Leone            
[151] Singapore                Soloman-Islands          Somalia                 
[154] South-Africa             South-Korea              South-Yemen             
[157] Spain                    Sri-Lanka                St-Helena               
[160] St-Kitts-Nevis           St-Lucia                 St-Vincent              
[163] Sudan                    Surinam                  Swaziland               
[166] Sweden                   Switzerland              Syria                   
[169] Taiwan                   Tanzania                 Thailand                
[172] Togo                     Tonga                    Trinidad-Tobago         
[175] Tunisia                  Turkey                   Turks-Cocos-Islands     
[178] Tuvalu                   UAE                      Uganda                  
[181] UK                       Uruguay                  US-Virgin-Isles         
[184] USA                      USSR                     Vanuatu                 
[187] Vatican-City             Venezuela                Vietnam                 
[190] Western-Samoa            Yugoslavia               Zaire                   
[193] Zambia                   Zimbabwe                
194 Levels: Afghanistan Albania Algeria American-Samoa Andorra Angola ... Zimbabwe

$landmass
  [1] 5 3 4 6 3 4 1 1 2 2 6 3 1 5 5 1 3 1 4 1 5 2 4 2 1 5 3 4 5 4 4 1 4 1 4 4 2 5 2
 [40] 4 4 6 1 1 3 3 3 4 1 1 2 4 1 4 4 3 2 6 3 3 2 6 4 4 3 3 4 3 3 1 1 6 1 4 4 2 1 1
 [79] 5 3 3 5 6 5 5 3 5 3 4 1 5 5 5 4 6 5 5 5 4 4 4 3 3 4 4 5 5 4 3 6 4 4 1 6 3 5 1
[118] 4 4 6 5 3 1 6 1 4 4 6 5 5 3 5 5 2 6 2 2 6 3 3 1 5 3 4 3 4 5 4 4 4 5 6 4 4 5 5
[157] 3 5 4 1 1 1 4 2 4 3 3 5 5 4 5 4 6 2 4 5 1 6 5 4 3 2 1 1 5 6 3 2 5 6 3 4 4 4

$zone
  [1] 1 1 1 3 1 2 4 4 3 3 2 1 4 1 1 4 1 4 1 4 1 3 2 3 4 1 1 4 1 2 1 4 4 4 1 1 3 1 4
 [40] 2 2 3 4 4 1 1 1 1 4 4 3 1 4 1 1 4 3 2 1 1 4 3 2 4 1 1 4 4 1 4 4 1 4 4 4 4 4 4
 [79] 1 1 4 1 2 1 1 4 1 1 4 4 1 1 1 1 1 1 1 1 2 4 1 1 1 2 2 1 1 4 1 1 4 2 4 1 1 1 4
[118] 4 2 2 1 1 4 2 4 1 1 3 1 1 1 1 1 4 2 3 3 1 1 4 4 1 1 2 1 1 1 4 2 4 1 2 1 2 1 1
[157] 4 1 3 4 4 4 1 4 2 1 1 1 1 2 1 1 2 4 1 1 4 2 1 1 4 3 4 4 1 2 1 4 1 3 1 2 2 2

$area
  [1]   648    29  2388     0     0  1247     0     0  2777  2777  7690    84    19
 [14]     1   143     0    31    23   113     0    47  1099   600  8512     0     6
 [27]   111   274   678    28   474  9976     4     0   623  1284   757  9561  1139
 [40]     2   342     0    51   115     9   128    43    22     0    49   284  1001
 [53]    21    28  1222     1    12    18   337   547    91     4   268    10   108
 [66]   249   239     0   132  2176     0     0   109   246    36   215    28   112
 [79]     1    93   103  3268  1904  1648   435    70    21   301   323    11   372
 [92]    98   181   583     0    18   236    10    30   111  1760     0     3   587
[105]   118   333     0  1240     0     0  1031     2  1973     1     0  1566     0
[118]   447   783     0   140    41     0   268   128  1267   925     0   121   195
[131]   324   212   804    76   463   407  1285   300   313    92     9    11   237
[144]    26     0     0  2150   196     0    72     1    30   637  1221    99   288
[157]   505    66     0     0     0     0  2506    63    17   450    41   185    36
[170]   945   514    57     1     5   164   781     0     0    84   236   245   178
[183]     0  9363 22402    15     0   912   333     3   256   905   753   391

$population
  [1]   16    3   20    0    0    7    0    0   28   28   15    8    0    0   90
 [16]    0   10    0    3    0    1    6    1  119    0    0    9    7   35    4
 [31]    8   24    0    0    2    4   11 1008   28    0    2    0    2   10    1
 [46]   15    5    0    0    6    8   47    5    0   31    0    0    1    5   54
 [61]    0    0    1    1   17   61   14    0   10    0    0    0    8    6    1
 [76]    1    6    4    5   11    0  684  157   39   14    3    4   57    7    2
 [91]  118    2    6   17    0    2    3    3    1    1    3    0    0    9    6
[106]   13    0    7    0    0    2    1   77    0    0    2    0   20   12    0
[121]   16   14    0    2    3    5   56    0   18    9    4    1   84    2    3
[136]    3   14   48   36   10    3    0   22    5    0    0    9    6    0    3
[151]    3    0    5   29   39    2   38   15    0    0    0    0   20    0    1
[166]    8    6   10   18   18   49    2    0    1    7   45    0    0    1   13
[181]   56    3    0  231  274    0    0   15   60    0   22   28    6    8

$language
  [1] 10  6  8  1  6 10  1  1  2  2  1  4  1  8  6  1  6  1  3  1 10  2 10  6  1 10
 [27]  5  3 10 10  3  1  6  1 10  3  2  7  2  3 10  1  2  2  6  5  6  3  1  2  2  8
 [53]  2 10 10  6  1  1  9  3  3  3 10  1  4  4  1  1  6  6  1  1  2  3  6  1  3  2
 [79]  7  9  6  6 10  6  8  1 10  6  3  1  9  8 10 10  1  8 10  8 10 10  8  4  4 10
[105] 10 10 10  3 10 10  8  1  2 10  3 10  1  8 10 10 10  6  6  1  2  3 10  1 10  8
[131]  6  8  6  2  1  2  2 10  5  6  2  8  6 10  6  6  8  3  1  1  7  1 10  6 10  8
[157]  2 10  1  1  1  1  8  6 10  6  4  8  7 10 10  3 10  1  8  9  1  1  8 10  1  2
[183]  1  1  5  6  6  2 10  1  6 10 10 10

$religion
  [1] 2 6 2 1 0 5 1 1 0 0 1 0 1 2 2 1 0 1 5 1 3 0 5 0 1 2 6 5 3 5 1 1 0 1 5 5 0 6 0
 [40] 2 5 1 0 6 1 6 1 2 1 0 0 2 0 5 1 1 1 1 1 0 0 0 5 5 6 1 5 1 1 1 1 1 0 2 5 4 0 0
 [79] 3 6 1 4 2 2 2 0 7 0 5 1 7 2 3 5 1 2 6 2 5 5 2 0 0 1 5 2 2 2 0 1 2 4 0 1 0 6 1
[118] 2 5 1 4 1 1 1 0 2 2 1 6 2 1 2 2 0 5 0 0 0 6 0 0 2 6 5 0 0 2 2 1 5 3 1 2 1 7 2
[157] 0 3 1 1 1 1 2 1 1 1 1 2 3 5 3 7 1 1 2 2 1 1 2 5 1 0 1 1 6 1 0 0 6 1 6 5 5 5

$bars
  [1] 0 0 2 0 3 0 0 0 0 0 0 0 0 0 0 3 3 0 0 0 0 0 0 0 0 0 0 0 0 0 3 2 1 0 1 3 0 0 0
 [40] 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 3 3 0 0 0 0 0 0 0 0 0 0 0 3 3 1 0 2 0
 [79] 0 0 0 0 0 0 0 3 0 3 3 0 0 0 0 0 0 0 0 0 2 0 0 0 0 1 0 0 0 3 2 0 0 0 3 0 0 3 0
[118] 0 0 0 0 0 0 0 0 0 3 0 0 0 0 0 1 0 0 0 3 0 0 0 0 0 3 3 0 0 0 3 0 0 0 0 0 0 0 0
[157] 0 2 0 0 0 5 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 1 0 0 0 0 0 0 0 2 0 0 0 0 0 3 0

$stripes
  [1]  3  0  0  0  0  2  1  1  3  3  0  3  3  0  0  0  0  2  0  0  0  3  5  0  0  0
 [27]  3  2  0  0  0  0  2  0  0  0  2  0  3  0  0  0  5  5  0  0  0  0  0  0  3  3
 [53]  3  3  3  0  0  0  0  0  0  3  3  5  3  3  3  1  9  0  0  0  0  0  2  0  0  3
 [79]  0  3  0  3  2  3  3  0  2  0  0  0  0  3  0  5  0  3  3  2  0 11  0  2  3  2
[105]  3 14  0  0  0  0  0  4  0  0  2  0  0  0  5  3  0  3  1  0  3  3  0  0  5  3
[131]  0  2  0  0  0  3  0  0  2  0  5  0  0  0  2  3  0  0  0  3  2  0  0  3  0  3
[157]  3  0  0  0  0  0  3  5  5  0  0  3  0  0  5  5  0  0  0  0  0  0  3  6  0  9
[183]  0 13  0  0  0  3  0  0  3  0  0  7

$colours
  [1] 5 3 3 5 3 3 3 5 2 3 3 2 3 2 2 3 3 8 2 6 4 3 3 4 6 4 5 3 3 3 3 2 5 6 5 3 3 2 3
 [40] 2 3 4 3 3 3 3 2 4 6 3 3 4 2 4 3 3 6 7 2 3 3 5 3 4 3 3 4 3 2 2 3 7 2 3 4 5 2 2
 [79] 6 3 3 4 2 3 4 3 2 3 3 3 2 4 2 4 4 4 3 4 4 3 1 3 3 3 3 4 3 3 3 3 2 4 4 2 2 3 7
[118] 2 5 3 3 3 3 3 2 3 2 4 3 4 3 3 2 3 4 6 2 4 2 5 3 2 7 4 2 4 2 3 3 3 2 4 2 5 4 4
[157] 2 4 7 5 4 4 4 4 7 2 2 4 3 4 3 4 2 3 2 2 6 5 4 5 3 3 6 3 2 4 4 7 2 3 4 4 4 5

$red
  [1] 1 1 1 1 1 1 0 1 0 0 1 1 0 1 1 0 1 1 1 1 1 1 0 0 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1
 [40] 0 1 1 1 1 0 1 1 1 1 1 1 1 0 1 1 1 1 1 0 1 1 1 0 1 1 1 1 1 0 1 1 1 0 1 1 1 1 0
 [79] 1 1 1 0 1 1 1 0 0 1 1 0 1 1 1 1 1 1 1 1 1 1 0 1 1 1 1 1 1 1 1 0 0 1 1 0 1 1 1
[118] 1 1 0 0 1 1 1 0 0 0 1 1 1 1 1 0 1 1 1 1 1 1 1 1 0 1 1 0 1 0 1 1 0 1 0 0 1 1 1
[157] 1 0 1 1 0 0 1 1 1 0 1 1 1 0 1 1 1 1 1 1 1 1 1 1 1 0 1 1 1 1 1 1 1 1 1 1 1 1

$green
  [1] 1 0 1 0 0 0 0 0 0 0 0 0 0 0 1 0 0 1 1 1 0 1 0 1 1 0 1 1 0 1 1 0 1 1 1 0 0 0 0
 [40] 1 1 0 0 0 1 0 0 1 1 0 0 0 0 1 1 0 1 1 0 0 0 0 1 1 0 0 1 0 0 0 1 1 0 1 1 1 0 0
 [79] 1 1 0 1 0 1 1 1 0 1 1 1 0 1 0 1 0 1 0 1 1 0 1 0 0 1 1 0 1 1 0 0 1 1 1 0 0 0 1
[118] 1 1 0 0 0 0 0 0 1 1 0 0 1 0 1 1 0 0 1 0 0 0 1 0 0 1 1 0 1 1 1 1 1 0 1 0 1 0 0
[157] 0 1 1 1 0 1 1 1 0 0 0 1 0 1 0 1 0 0 0 0 1 0 1 0 0 0 1 0 0 1 0 1 0 0 0 1 1 1

$blue
  [1] 0 0 0 1 1 0 1 1 1 1 1 0 1 0 0 1 0 1 0 1 0 0 1 1 1 0 1 0 1 0 0 0 0 1 1 1 1 0 1
 [40] 0 0 1 1 1 0 1 0 1 1 1 1 0 1 1 0 1 1 1 1 1 1 1 1 1 0 0 0 0 1 0 0 1 1 0 0 0 0 1
 [79] 1 0 1 1 0 0 0 0 1 0 0 0 0 0 0 0 1 0 1 0 1 1 0 1 1 0 0 1 0 0 0 1 0 1 0 1 0 1 1
[118] 0 0 1 1 1 1 1 1 0 0 1 1 0 1 0 0 1 0 1 0 1 0 1 1 0 1 0 1 0 0 0 0 1 0 1 1 1 1 1
[157] 0 0 1 0 1 1 0 0 1 1 0 0 1 1 1 0 0 0 0 0 1 1 0 0 1 1 1 1 0 0 0 1 0 1 1 0 0 0

$gold
  [1] 1 1 0 1 1 1 0 1 0 1 0 0 1 0 0 1 1 1 0 1 0 1 0 1 1 1 1 1 0 0 1 0 1 1 1 1 0 1 1
 [40] 0 1 0 0 0 1 0 0 0 1 0 1 1 0 0 1 0 1 1 0 0 0 1 1 0 1 1 1 1 0 0 1 1 0 1 1 1 0 0
 [79] 1 0 0 0 0 0 0 0 0 0 0 1 0 0 1 0 1 0 0 0 0 0 0 1 0 0 0 1 0 1 0 0 1 1 0 0 0 1 1
[118] 0 1 1 0 0 0 0 0 0 0 1 0 0 0 0 0 0 1 1 0 1 0 1 0 0 1 1 0 1 0 1 0 0 0 1 0 0 0 0
[157] 1 1 1 1 1 1 0 1 1 1 0 0 0 1 0 1 0 0 0 0 1 1 0 1 0 1 1 0 1 1 1 1 1 0 1 1 0 1

$white
  [1] 1 0 1 1 0 0 1 1 1 1 1 1 0 1 0 0 0 1 0 1 1 0 1 1 1 1 1 0 1 1 0 1 0 1 1 0 1 0 0
 [40] 1 0 1 1 1 1 1 1 1 1 1 0 1 1 1 0 1 1 1 1 1 1 1 0 1 0 0 0 1 1 1 0 1 1 0 0 1 0 1
 [79] 1 1 1 1 1 1 1 1 1 1 1 0 1 1 0 1 1 1 1 1 1 1 0 0 1 1 0 1 1 0 1 1 0 0 1 1 1 0 1
[118] 0 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 0 1 0 1 0 1 1 1 1 1 1 1 1
[157] 0 0 1 1 1 1 1 1 1 0 1 1 1 0 1 1 1 1 1 1 1 1 1 1 1 1 1 1 0 0 1 1 0 1 1 0 0 1

$black
  [1] 1 1 0 0 0 1 0 1 0 0 0 0 1 0 0 1 1 1 0 1 1 0 1 0 0 1 0 0 0 0 0 0 1 0 0 0 0 0 0
 [40] 0 0 0 0 0 0 0 0 0 1 0 0 1 0 0 0 0 0 0 0 0 0 1 0 0 1 1 1 0 0 0 0 0 0 0 1 1 1 0
 [79] 0 0 0 0 0 0 1 0 0 0 0 1 0 1 0 1 0 1 0 0 0 0 0 0 0 0 1 0 0 0 1 0 0 0 0 0 0 0 1
[118] 0 1 0 0 0 0 0 0 0 0 0 0 1 0 0 0 0 1 1 0 0 0 0 0 0 0 1 0 1 0 0 0 0 0 0 0 0 1 1
[157] 0 0 0 1 1 0 1 0 1 0 0 1 0 1 0 0 0 1 0 0 0 0 1 1 0 0 0 0 0 1 1 1 0 0 0 0 1 1

$orange
  [1] 0 0 0 1 0 0 1 0 0 0 0 0 0 0 0 0 0 1 0 0 1 0 0 0 1 0 0 0 0 0 0 0 1 1 0 0 0 0 0
 [40] 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 1 0 0 0 0 0 0 0 0 0 0 0 0 0 1 0 0 0 0 0 0
 [79] 1 0 0 1 0 0 0 1 0 0 0 0 0 0 0 0 0 0 0 1 0 0 0 0 0 0 0 0 0 0 0 0 0 0 1 0 0 0 0
[118] 0 0 0 1 0 0 0 0 1 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 1 1 0 0 0 0 0 0 0 0 0 0 1 0 0
[157] 0 1 1 0 0 0 0 0 1 0 0 0 0 0 0 0 0 0 0 0 1 0 0 0 0 0 0 0 0 0 0 1 0 0 0 1 1 0

$mainhue
  [1] green  red    green  blue   gold   red    white  red    blue   blue   blue  
 [12] red    blue   red    green  blue   gold   blue   green  red    orange red   
 [23] blue   green  blue   gold   red    red    red    red    gold   red    gold  
 [34] blue   gold   gold   red    red    gold   green  red    blue   blue   blue  
 [45] white  white  red    blue   green  blue   gold   black  blue   green  green 
 [56] white  blue   blue   white  white  white  red    green  red    gold   black 
 [67] red    white  blue   white  gold   blue   blue   gold   gold   green  black 
 [78] blue   blue   red    blue   orange red    red    red    white  white  white 
 [89] white  green  white  black  red    red    red    green  red    red    blue  
[100] red    green  red    red    red    red    red    red    gold   red    blue  
[111] green  red    green  blue   red    red    blue   red    gold   blue   brown 
[122] red    white  blue   blue   orange green  gold   blue   red    red    red   
[133] green  red    black  red    red    blue   white  red    red    brown  red   
[144] red    white  green  green  green  red    green  white  green  blue   orange
[155] white  red    red    gold   blue   green  blue   green  red    red    blue  
[166] blue   red    red    red    green  red    green  red    red    red    red   
[177] blue   blue   green  gold   red    white  white  white  red    red    gold  
[188] red    red    red    red    green  green  green 
Levels: black blue brown gold green orange red white

$circles
  [1] 0 0 0 0 0 0 0 0 0 0 0 0 0 0 1 0 0 1 0 1 4 0 0 1 0 0 0 0 0 1 0 0 0 1 0 0 0 0 0
 [40] 0 0 1 0 0 0 0 0 0 1 0 0 0 0 0 0 0 1 0 0 0 0 1 0 0 0 0 0 0 0 1 1 0 0 0 0 0 0 0
 [79] 1 0 0 1 0 0 0 0 0 0 0 0 1 0 0 1 0 0 1 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 2 0
[118] 0 0 0 0 0 0 0 0 1 0 1 1 0 0 0 0 0 0 1 0 0 0 1 0 0 0 0 0 0 0 0 0 0 0 0 0 0 1 0
[157] 0 0 0 0 0 0 0 0 0 0 0 0 1 0 0 0 0 0 1 0 0 0 0 1 0 0 0 0 0 0 0 0 0 0 0 1 0 0

$crosses
  [1] 0 0 0 0 0 0 0 0 0 0 1 0 0 0 0 0 0 0 0 1 0 0 0 0 1 0 0 0 0 0 0 0 0 1 0 0 0 0 0
 [40] 0 0 1 0 0 0 0 1 0 0 1 0 0 0 0 0 1 1 2 1 0 0 0 0 0 0 0 0 0 1 0 0 0 0 0 0 0 0 0
 [79] 1 0 1 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 1 0 0 0 0 0 0 0 2
[118] 0 0 0 0 0 0 1 0 0 0 1 0 0 1 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 1 0 0
[157] 0 0 1 0 0 0 0 0 0 1 1 0 0 0 0 0 1 0 0 0 1 1 0 0 1 0 0 0 0 0 0 0 0 0 0 0 0 0

$saltires
  [1] 0 0 0 0 0 0 0 0 0 0 1 0 0 0 0 0 0 0 0 1 0 0 0 0 1 0 0 0 0 1 0 0 0 1 0 0 0 0 0
 [40] 0 0 1 0 0 0 0 0 0 0 0 0 0 0 0 0 0 1 1 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0
 [79] 1 0 0 0 0 0 0 0 0 0 0 1 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 1
[118] 0 0 0 0 0 0 1 0 0 0 1 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 1 0 0
[157] 0 0 1 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 1 1 0 0 1 0 0 0 0 0 0 0 0 0 0 0 0 0

$quarters
  [1] 0 0 0 0 0 0 0 0 0 0 1 0 0 0 0 0 0 0 0 1 0 0 0 0 1 0 0 0 1 0 0 0 0 1 0 0 1 0 0
 [40] 0 0 1 0 0 0 0 0 0 0 0 0 0 0 0 0 0 1 1 0 0 0 0 0 0 0 0 0 0 1 0 0 0 0 0 0 0 0 0
 [79] 1 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 1 0 0 0 0 0 1 0 0 0 0 0 0 0 0 0 0 1
[118] 0 0 0 0 0 0 1 0 0 0 1 0 0 0 0 0 4 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0
[157] 0 0 1 0 0 0 0 0 0 0 0 0 1 0 0 1 1 0 0 0 1 1 0 0 0 1 0 1 0 0 0 0 0 1 0 0 0 0

$sunstars
  [1]  1  1  1  0  0  1  0  1  0  1  6  0  0  0  0  0  0  0  1  0  0  0  0 22  0  0
 [27]  1  1 14  3  1  0  1  4  1  0  1  5  0  4  1 15  0  1  0  0  0  1 10  0  0  0
 [53]  0  0  0  0  0  0  0  0  0  1  0  0  0  0  1  0  0  0  7  0  0  0  1  0  0  5
 [79]  0  0  0  0  0  0  3  0  1  0  0  0  1  1  0  0  1  0  0  0  0  1  0  0  0  0
[105]  1  1  0  0  0  1  1  0  0  4  0  1  0  1  1  1  2  0  6  4  0  0  0  5  1  1
[131]  0  0  1  2  5  1  0  4  0  0  1  0  2  0  0  2  0  1  0  0  5  5  1  0  0  1
[157]  0  0  0  2  0  0  0  1  0  0  0  2  1  0  0  1  0  0  1  1  0  9  0  0  0  1
[183]  0 50  1  0  0  7  1  5  1  0  0  1

$crescent
  [1] 0 0 1 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0
 [40] 1 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0
 [79] 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 1 1 0 0 0 1 0 0 0 0 1 0
[118] 0 0 0 1 0 0 0 0 0 0 0 0 0 0 0 1 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 1 0 0 0 0 0
[157] 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 1 1 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0

$triangle
  [1] 0 0 0 1 0 0 0 1 0 0 0 0 1 0 0 0 0 0 0 0 0 0 0 0 0 1 0 0 0 0 0 0 0 0 0 0 0 0 0
 [40] 0 0 0 0 1 0 1 0 1 0 0 0 0 0 1 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 1 0 0 0 0 1 0 0
 [79] 0 0 0 0 0 0 0 0 0 0 0 1 0 1 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 1 0
[118] 0 1 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 1 0 0 1 0 0 1 0 0 0 0 1 0 0 0 0 0 1 0 0 0 1
[157] 0 0 0 1 1 0 1 0 0 0 0 0 0 1 0 0 0 1 0 0 0 0 0 0 0 0 0 0 0 1 0 0 0 0 0 0 0 1

$icon
  [1] 1 0 0 1 0 1 0 0 0 0 0 0 0 0 0 1 0 1 0 1 0 0 0 0 1 1 1 0 1 0 0 0 0 1 0 0 0 0 0
 [40] 0 1 0 0 0 1 0 0 0 0 0 0 0 0 0 0 0 1 1 0 0 0 1 0 0 1 0 0 1 0 0 0 1 0 0 0 0 0 0
 [79] 1 0 0 1 0 1 0 0 0 0 0 0 0 0 1 1 1 0 0 0 1 0 0 1 0 0 0 0 0 0 1 1 0 0 0 0 0 1 1
[118] 0 1 0 0 0 0 0 0 0 0 0 0 0 0 1 0 0 0 1 0 0 0 1 0 0 1 0 0 0 1 0 0 0 0 0 0 0 1 0
[157] 0 1 1 0 0 1 0 0 1 0 0 0 0 0 0 0 0 0 0 0 1 0 0 0 0 0 1 0 1 0 1 1 0 0 0 1 0 1

$animate
  [1] 0 1 0 1 0 0 1 0 0 0 0 0 0 0 0 0 0 1 0 1 1 0 0 0 1 1 1 0 1 0 0 1 1 1 0 0 0 0 0
 [40] 0 1 0 0 0 1 0 0 0 1 0 0 1 0 0 0 0 1 1 0 0 0 0 0 0 0 0 0 0 0 0 1 1 0 0 0 0 0 0
 [79] 1 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 1 0 0 1 0 0 0 0 0 0 0 0 0 0 0 0 0 0 1 0 0 0 1
[118] 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 1 1 0 0 0 0 0 0 1 0 0 0 0 0 0 0 0 0 0 0 0 0
[157] 0 1 0 0 0 1 0 0 0 0 0 0 0 0 0 0 0 0 0 0 1 0 0 1 0 0 1 0 0 1 0 1 0 0 0 1 1 1

$text
  [1] 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 1 0 0 0 0 0 1 1 1 0 0 0 0 0 0 0 1 0 0 0 0 0
 [40] 0 0 0 0 0 0 0 0 0 0 0 0 1 0 0 0 0 1 0 0 0 0 0 0 0 0 0 0 0 0 0 0 1 0 0 0 0 0 0
 [79] 1 0 0 0 0 1 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0
[118] 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 1 0 0 0 0 0 0 1 1 0 0 1 0 0 0 0 0 0 0 0 0
[157] 0 0 0 0 0 1 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 1 0 0 0 0 0 0 0 0 0 0 0

$topleft
  [1] black  red    green  blue   blue   red    white  black  blue   blue   white 
 [12] red    blue   white  green  blue   black  red    green  white  orange red   
 [23] blue   green  white  white  white  red    blue   white  green  red    red   
 [34] white  blue   blue   blue   red    gold   green  red    white  blue   blue  
 [45] white  white  red    white  green  blue   gold   red    blue   green  green 
 [56] white  white  white  white  blue   blue   red    green  red    black  black 
 [67] red    white  blue   white  red    red    blue   red    red    black  black 
 [78] blue   white  red    blue   orange red    green  red    green  blue   green 
 [89] red    gold   white  black  red    black  red    green  red    red    green 
[100] blue   green  blue   red    white  black  blue   red    green  white  blue  
[111] green  red    green  blue   red    red    white  red    green  blue   blue  
[122] red    white  white  blue   orange green  white  blue   red    red    red   
[133] white  white  red    red    red    blue   white  green  red    white  blue  
[144] red    white  green  green  green  red    green  red    blue   blue   orange
[155] white  red    red    gold   white  green  blue   blue   red    green  blue  
[166] blue   red    red    blue   green  red    red    white  white  red    red   
[177] white  white  red    black  white  white  white  blue   red    black  gold  
[188] gold   red    blue   blue   green  green  green 
Levels: black blue gold green orange red white

$botright
  [1] green  red    white  red    red    black  blue   red    blue   blue   blue  
 [12] red    blue   red    green  blue   red    red    green  red    red    green 
 [23] blue   green  blue   gold   red    green  red    white  gold   red    green 
 [34] blue   gold   red    red    red    red    green  red    blue   blue   blue  
 [45] white  red    red    green  green  blue   red    black  blue   red    red   
 [56] white  blue   blue   white  red    red    red    blue   green  gold   gold  
 [67] green  red    blue   red    red    red    blue   green  green  green  red   
 [78] blue   blue   green  blue   green  white  red    black  orange blue   red   
 [89] green  gold   white  green  red    green  blue   red    red    red    blue  
[100] red    green  red    blue   green  green  white  red    red    red    blue  
[111] green  green  red    blue   white  red    blue   red    gold   blue   blue  
[122] blue   white  blue   blue   green  green  gold   blue   black  red    green 
[133] green  white  black  blue   red    red    red    red    red    brown  red   
[144] green  blue   green  green  red    green  blue   white  green  blue   blue  
[155] white  black  red    gold   blue   red    blue   green  black  green  blue  
[166] blue   red    black  red    blue   red    green  red    white  red    red   
[177] blue   blue   black  red    red    white  white  red    red    green  white 
[188] red    red    red    red    green  brown  green 
Levels: black blue brown gold green orange red white
```
## lapply()
To apply the class() function to each column of the flags dataset and store the result in a variable called cls_list we will use the lapply() function. From this we will get a list of length 30 -- one element for each variable/column.

```
> cls_list <- lapply(flags, class)
> cls_list
$name
[1] "factor"

$landmass
[1] "integer"

$zone
[1] "integer"

$area
[1] "integer"

$population
[1] "integer"

$language
[1] "integer"

$religion
[1] "integer"

$bars
[1] "integer"

$stripes
[1] "integer"

$colours
[1] "integer"

$red
[1] "integer"

$green
[1] "integer"

$blue
[1] "integer"

$gold
[1] "integer"

$white
[1] "integer"

$black
[1] "integer"

$orange
[1] "integer"

$mainhue
[1] "factor"

$circles
[1] "integer"

$crosses
[1] "integer"

$saltires
[1] "integer"

$quarters
[1] "integer"

$sunstars
[1] "integer"

$crescent
[1] "integer"

$triangle
[1] "integer"

$icon
[1] "integer"

$animate
[1] "integer"

$text
[1] "integer"

$topleft
[1] "factor"

$botright
[1] "factor"
```

The 'l' in 'lapply' stands for 'list':
```
> class(cls_list)
[1] "list"
```

The 'l' in 'lapply' stands for 'list':
```
> class(cls_list)
[1] "list"
```

In this case, since every element of the list returned by lapply() is a character vector of length one (i.e. "integer" and "vector"), cls_list can be simplified to a character vector:
```
> as.character(cls_list)
 [1] "factor"  "integer" "integer" "integer" "integer" "integer" "integer"
 [8] "integer" "integer" "integer" "integer" "integer" "integer" "integer"
[15] "integer" "integer" "integer" "factor"  "integer" "integer" "integer"
[22] "integer" "integer" "integer" "integer" "integer" "integer" "integer"
[29] "factor"  "factor" 
```

## sapply()

sapply() allows you to automate this process by calling lapply() behind the scenes, but then attempting to simplify (hence the 's' in 'sapply') the result for you. 

```
> cls_vect <- sapply(flags, class)

> class(cls_vect)
[1] "character"

> cls_vect
      name   landmass       zone       area population   language   religion 
  "factor"  "integer"  "integer"  "integer"  "integer"  "integer"  "integer" 
      bars    stripes    colours        red      green       blue       gold 
 "integer"  "integer"  "integer"  "integer"  "integer"  "integer"  "integer" 
     white      black     orange    mainhue    circles    crosses   saltires 
 "integer"  "integer"  "integer"   "factor"  "integer"  "integer"  "integer" 
  quarters   sunstars   crescent   triangle       icon    animate       text 
 "integer"  "integer"  "integer"  "integer"  "integer"  "integer"  "integer" 
   topleft   botright 
  "factor"   "factor" 
```

In general, if the result is a list where every element is of length one, then sapply() returns a vector. If the result is a list where every element is a vector of the same length (> 1), sapply() returns a matrix. If sapply() can't figure things out, then it just returns a list, no different from what lapply() would give you.

##### An example:
Columns 11 through 17 of our dataset are indicator variables, each representing a different color. The value of the indicator variable is 1 if the color is present in a country's flag and 0 otherwise.
```
> cls_vect[11:17]
      red     green      blue      gold     white     black    orange 
"integer" "integer" "integer" "integer" "integer" "integer" "integer" 
```

if we want to know the total number of countries (in our dataset) with, for example, the color orange on their flag:
```
> sum(flags$orange)
[1] 26
```

To repeat this operation for each of the colors recorded in the dataset.
First we extract the columns containing the color data and store them in a new data frame called flag_colors.
```
> flag_colors <- flags[, 11:17]
> head(flag_colors )
  red green blue gold white black orange
1   1     1    0    1     1     1      0
2   1     0    0    1     0     1      0
3   1     1    0    0     1     0      0
4   1     0    1    1     1     0      1
5   1     0    1    1     0     0      0
6   1     0    0    1     0     1      0
```

To get a list containing the sum of each column of flag_colors, call the lapply() function with two arguments. The first argument is the object over which we are looping (i.e. flag_colors) and the second argument is the name of the function we wish to apply to each column (i.e. sum). Remember that the second argument is just the name of the function with no parentheses, etc.
```
> lapply(flag_colors, sum)
$red
[1] 153

$green
[1] 91

$blue
[1] 99

$gold
[1] 91

$white
[1] 146

$black
[1] 52

$orange
[1] 26
```

The result is a list, since lapply() always returns a list. Each element of this list is of length one, so the result can be simplified to a vector by calling sapply() instead of lapply().
```
> sapply(flag_colors, sum)
   red  green   blue   gold  white  black orange 
   153     91     99     91    146     52     26 

> sapply(flag_colors, mean)
      red     green      blue      gold     white     black    orange 
0.7886598 0.4690722 0.5103093 0.4690722 0.7525773 0.2680412 0.1340206 
```

Let's extract columns 19 through 23 from the flags dataset.  Each of these columns (i.e. variables) represents the number of times a particular shape or design appears on a country's flag. We are interested in the minimum and maximum number of times each shape or design appears.
```
> flag_shapes <- flags[, 19:23]
> head(flag_shapes)
  circles crosses saltires quarters sunstars
1       0       0        0        0        1
2       0       0        0        0        1
3       0       0        0        0        1
4       0       0        0        0        0
5       0       0        0        0        0
6       0       0        0        0        1
```

The range() function returns the minimum and maximum of its first argument, which should be a numeric vector. Use lapply() to apply the range function to each column of flag_shapes.
```
> lapply(flag_shapes, range)
$circles
[1] 0 4

$crosses
[1] 0 2

$saltires
[1] 0 1

$quarters
[1] 0 4

$sunstars
[1]  0 50
```

Do the same operation, but using sapply() and store the result in a variable called shape_mat. Each column of shape_mat gives the minimum (row 1) and maximum (row 2) number of times its respective shape appears in different flags.
```
> shape_mat <- sapply(flag_shapes, range)

> shape_mat
     circles crosses saltires quarters sunstars
[1,]       0       0        0        0        0
[2,]       4       2        1        4       50


> class(shape_mat)
[1] "matrix"
```

##### Another example:
When given a vector, the unique() function returns a vector with all duplicate elements removed. In other words, unique() returns a vector of only the 'unique' elements.
```
> unique(c(3, 4, 5, 5, 5, 6, 6))
[1] 3 4 5 6

> unique_vals <- lapply(flags, unique)
> unique_vals
$name
  [1] Afghanistan              Albania                  Algeria                 
  [4] American-Samoa           Andorra                  Angola                  
  [7] Anguilla                 Antigua-Barbuda          Argentina               
 [10] Argentine                Australia                Austria                 
 [13] Bahamas                  Bahrain                  Bangladesh              
 [16] Barbados                 Belgium                  Belize                  
 [19] Benin                    Bermuda                  Bhutan                  
 [22] Bolivia                  Botswana                 Brazil                  
 [25] British-Virgin-Isles     Brunei                   Bulgaria                
 [28] Burkina                  Burma                    Burundi                 
 [31] Cameroon                 Canada                   Cape-Verde-Islands      
 [34] Cayman-Islands           Central-African-Republic Chad                    
 [37] Chile                    China                    Colombia                
 [40] Comorro-Islands          Congo                    Cook-Islands            
 [43] Costa-Rica               Cuba                     Cyprus                  
 [46] Czechoslovakia           Denmark                  Djibouti                
 [49] Dominica                 Dominican-Republic       Ecuador                 
 [52] Egypt                    El-Salvador              Equatorial-Guinea       
 [55] Ethiopia                 Faeroes                  Falklands-Malvinas      
 [58] Fiji                     Finland                  France                  
 [61] French-Guiana            French-Polynesia         Gabon                   
 [64] Gambia                   Germany-DDR              Germany-FRG             
 [67] Ghana                    Gibraltar                Greece                  
 [70] Greenland                Grenada                  Guam                    
 [73] Guatemala                Guinea                   Guinea-Bissau           
 [76] Guyana                   Haiti                    Honduras                
 [79] Hong-Kong                Hungary                  Iceland                 
 [82] India                    Indonesia                Iran                    
 [85] Iraq                     Ireland                  Israel                  
 [88] Italy                    Ivory-Coast              Jamaica                 
 [91] Japan                    Jordan                   Kampuchea               
 [94] Kenya                    Kiribati                 Kuwait                  
 [97] Laos                     Lebanon                  Lesotho                 
[100] Liberia                  Libya                    Liechtenstein           
[103] Luxembourg               Malagasy                 Malawi                  
[106] Malaysia                 Maldive-Islands          Mali                    
[109] Malta                    Marianas                 Mauritania              
[112] Mauritius                Mexico                   Micronesia              
[115] Monaco                   Mongolia                 Montserrat              
[118] Morocco                  Mozambique               Nauru                   
[121] Nepal                    Netherlands              Netherlands-Antilles    
[124] New-Zealand              Nicaragua                Niger                   
[127] Nigeria                  Niue                     North-Korea             
[130] North-Yemen              Norway                   Oman                    
[133] Pakistan                 Panama                   Papua-New-Guinea        
[136] Parguay                  Peru                     Philippines             
[139] Poland                   Portugal                 Puerto-Rico             
[142] Qatar                    Romania                  Rwanda                  
[145] San-Marino               Sao-Tome                 Saudi-Arabia            
[148] Senegal                  Seychelles               Sierra-Leone            
[151] Singapore                Soloman-Islands          Somalia                 
[154] South-Africa             South-Korea              South-Yemen             
[157] Spain                    Sri-Lanka                St-Helena               
[160] St-Kitts-Nevis           St-Lucia                 St-Vincent              
[163] Sudan                    Surinam                  Swaziland               
[166] Sweden                   Switzerland              Syria                   
[169] Taiwan                   Tanzania                 Thailand                
[172] Togo                     Tonga                    Trinidad-Tobago         
[175] Tunisia                  Turkey                   Turks-Cocos-Islands     
[178] Tuvalu                   UAE                      Uganda                  
[181] UK                       Uruguay                  US-Virgin-Isles         
[184] USA                      USSR                     Vanuatu                 
[187] Vatican-City             Venezuela                Vietnam                 
[190] Western-Samoa            Yugoslavia               Zaire                   
[193] Zambia                   Zimbabwe                
194 Levels: Afghanistan Albania Algeria American-Samoa Andorra Angola ... Zimbabwe

$landmass
[1] 5 3 4 6 1 2

$zone
[1] 1 3 2 4

$area
  [1]   648    29  2388     0  1247  2777  7690    84    19     1   143    31    23
 [14]   113    47  1099   600  8512     6   111   274   678    28   474  9976     4
 [27]   623  1284   757  9561  1139     2   342    51   115     9   128    43    22
 [40]    49   284  1001    21  1222    12    18   337   547    91   268    10   108
 [53]   249   239   132  2176   109   246    36   215   112    93   103  3268  1904
 [66]  1648   435    70   301   323    11   372    98   181   583   236    30  1760
 [79]     3   587   118   333  1240  1031  1973  1566   447   783   140    41  1267
 [92]   925   121   195   324   212   804    76   463   407  1285   300   313    92
[105]   237    26  2150   196    72   637  1221    99   288   505    66  2506    63
[118]    17   450   185   945   514    57     5   164   781   245   178  9363 22402
[131]    15   912   256   905   753   391

$population
 [1]   16    3   20    0    7   28   15    8   90   10    1    6  119    9   35
[16]    4   24    2   11 1008    5   47   31   54   17   61   14  684  157   39
[31]   57  118   13   77   12   56   18   84   48   36   22   29   38   49   45
[46]  231  274   60

$language
 [1] 10  6  8  1  2  4  3  5  7  9

$religion
[1] 2 6 1 0 5 3 4 7

$bars
[1] 0 2 3 1 5

$stripes
 [1]  3  0  2  1  5  9 11 14  4  6 13  7

$colours
[1] 5 3 2 8 6 4 7 1

$red
[1] 1 0

$green
[1] 1 0

$blue
[1] 0 1

$gold
[1] 1 0

$white
[1] 1 0

$black
[1] 1 0

$orange
[1] 0 1

$mainhue
[1] green  red    blue   gold   white  orange black  brown 
Levels: black blue brown gold green orange red white

$circles
[1] 0 1 4 2

$crosses
[1] 0 1 2

$saltires
[1] 0 1

$quarters
[1] 0 1 4

$sunstars
 [1]  1  0  6 22 14  3  4  5 15 10  7  2  9 50

$crescent
[1] 0 1

$triangle
[1] 0 1

$icon
[1] 1 0

$animate
[1] 0 1

$text
[1] 0 1

$topleft
[1] black  red    green  blue   white  orange gold  
Levels: black blue gold green orange red white

$botright
[1] green  red    white  black  blue   gold   orange brown 
Levels: black blue brown gold green orange red white
```

To know how many different values there are for each element of unique_vals:
```
> sapply(unique_vals, length)
      name   landmass       zone       area population   language   religion 
       194          6          4        136         48         10          8 
      bars    stripes    colours        red      green       blue       gold 
         5         12          8          2          2          2          2 
     white      black     orange    mainhue    circles    crosses   saltires 
         2          2          2          8          4          3          2 
  quarters   sunstars   crescent   triangle       icon    animate       text 
         3         14          2          2          2          2          2 
   topleft   botright 
         7          8 
```

If you use sapply(flags, unique) to apply the unique function to each column of flags, you will fail to simplify the result, thus obtaining the same result as with lapplay().
