* 80/100 맞음.
    - 원인을 몰랐지만 지현님 코드랑 비교해보면 file reading에서 차이나는 것 같음.
    - 지현님 코드는 huge.txt 입력 받자마자 처리하는 반면, 내 코드는 처리시간이 좀 걸림.
* testcase의 huge.txt는 snuc.org에서 검색하다가 어떤 분이 만들어놓은 거 복사해왔는데 누구껀지 모르겟음...;;;

# Homework 6
## 문서에 나와있는 내용은 질문 받지 않습니다. 꼼꼼히 읽어주세요.
#### 1. 목표     
그래프를 이용하여 지하철 노선도를 표현하고, 최단 경로(소요 시간을 최소로 하는 경로)를 구합니다.

#### 2. 문제     
이번 과제에서는 출발역과 도착역을 주면 최단 경로를 구해서 경로와 소요 시간을 출력하도록 합니다. 역 사이에 걸리는 시간은 각각 다르며, 갈아타는 시간은 5분으로 계산합니다.
또 이번 마지막 숙제는 뼈대코드를 제공하지 않습니다. 지금까지의 뼈대코드를 통해 익혔던 것을 총정리하면 충분히 작성할 수 있을 것입니다.

#### 3. 실행 방법        
$ java Subway [data]
    1.	반드시 Subway.java를 만들어 여기에 main method를 두도록 합니다.
    2.	data - 지하철 노선 데이터 파일명입니다.

#### 4. 역 정보 입력
 * 역 정보는 텍스트 파일로 받습니다.

*	data        
    - 먼저 역에 관한 정보를 입력합니다. 각 줄마다 고유 번호(이것은 문자열로써 unique해야 합니다)를 쓰고, 그 뒤에 역 이름과 호선을 공백으로 구분하여 입력합니다.
    
    - 이름이 같은 역이 있으면 갈아타는 역으로 처리합니다.
    
    
    - 그 다음에 역과 역 사이의 소요시간에 관한 정보를 입력합니다. 출발역, 도착역, 소요시간 순서로 입력하고, 인접한 역의 정보만 입력합니다. (인접이란 중간에 다른 역을 거치지 않고 갈 수 있는 것을 뜻합니다.) 
    
    - 응암순환같이 단방향 노선이 아닌 경우에는 양쪽방향을 모두 입력해야 합니다.
    두 가지 정보 사이는 빈 줄(blank line)을 두어 구분합니다.        

    - 입력 예제       

        >	810 암사 8      
        >	811 천호 8      
        >	...     
        >	820 복정 8      
        >	...     
        >	825 수진 8      
        >	826 모란 8      
        >	1221 수서 K2        
        >	1222 복정 K2        
        >	...     
        >	1231 미금 K2        
        >	1232 오리 K2        
        	      <- blank line     
        >	810 811 2       
        >	811 810 2       
        >	811 812 3       
        >	812 811 3       
        >	...     
        >	825 826 4       
        >	826 825 4       
        >	1221 1222 5     
        >	1222 1221 5     
        >	...     
        >	1231 1232 3     
        >   1232 1231 3     

* 위 예제에서 복정역은 8호선<->K2(분당)선 갈아타는 역이고, 갈아타는 역 사이의 edge(820 1222 순서쌍)는 정의하지 않습니다. 
<br>
<br>

#### 5. 입출력 형식화면과 키보드를 통해 수행합니다.
1.	입력
    - 출발역 이름과 도착역 이름을 한 칸 띄어서 한 줄에 한 쌍씩 씁니다.        
    - QUIT 를 입력하면 종료합니다.        

        > 종각 낙성대     
        > 혜화 잠실       
        > 녹번 길음       
        > QUIT

1.	출력    
    - 하나의 입력당 하나씩 화면상으로 출력합니다. command를 처리하면서 각각 경로와 소요 시간을 출력합니다. 다른 것은 아무것도 출력하지 않도록 합니다.
    - 출발역부터 시작해서 도착역까지 차례대로 각 역 이름을 space로 구분합니다. 갈아타는 경우에는 환승역 이름을 []로 둘러쌉니다. 물론 갈아타지 않는 경우에는 그냥 역 이름만 출력합니다.
    - $ java Subway data 로 실행하는 경우 (data는 수도권 지하철 노선도 파일이라고 가정,)
        > 종각 낙성대       
        > 종각 시청 [서울역] 숙대입구 삼각지 신용산 이촌        동작 총신대입구 [사당] 낙성대     
        > 33        
        > 혜화 잠실     
        > 혜화 동대문 [동대문운동장] 신당 상왕십리              왕십리 한양대 뚝섬 성수 건대입구 구의 강변              성내 잠실      
        > 30        
        > 회현 서대문       
        > 회현 명동 충무로 [동대문역사문화공원]                 을지로4가 종로3가 광화문 서대문       
        > 18        
        > QUIT      



#### 6. 참고사항
1.	충분히 효율적으로 구현해야 합니다. 예를 들어 역 수가 수천개라면 최단경로를 1초 내에 구할 수 있어야 합니다.
2.	역의 번호와 이름은 유일합니다. (다만 환승역끼리는 이름이 같습니다)
3.	위에서 든 예에는 고유번호(역번호)가 숫자로 되어 있지만 문자인 경우도 처리할 수 있어야 합니다.
4.	교재, 강의노트의 코드나 자바 표준 API를 이용해도 좋습니다. 하지만 그 밖의 것은 직접 만들도록 합니다.
5.	자유롭게 할수 있으니만큼 입출력 형식을 틀리지 않도록 주의하기 바랍니다. (특히 출력할 때 뒤에 쓸모없는 공백을 추가하는 것)


#### 7. 자주 묻는 질문(필독!!!)
1. 테스트용 데이터      
http://gangwon.github.io/subway-data/ 에서 받으실 수 있습니다.
채점에 사용되는 데이터는 위의 데이터를 포함하여 여러 종류의 데이터를 사용함에 유의하시기 바랍니다.
    
1. 지하철 데이터의 형식     
역 이름, 역 번호, 노선 번호는 공백이 포함되지 않는 일반적인 문자열입니다.
역 '번호', 노선 '번호'이지만 숫자가 아닌 문자열도 입력됩니다.
역 간 거리는 음이 아닌 정수입니다. 즉, 두 역 사이의 거리가 0인 경우도 있을 수 있습니다.
    
1. 지하철 데이터의 크기     
역의 수는 최대 수 만개 정도입니다.
간선의 수는 최대 수십만개 정도입니다.
두 역 사이 간선의 거리(소요시간)는 1억 이하입니다.
한 역은 최대 수십개 정도의 노선이 지날 수 있습니다.
    
1. 입력의 제한      
입력되는 출발역 및 도착역은 모두 데이터에 존재하는 역이고, 항상 출발역과 도착역 사이에는 경로가 있습니다. 두 역이 같은 경우는 입력되지 않습니다.
    
1. 답이 여러 가지인 경우        
모범답안과 소요시간이 같고 올바른 경로인 경우 역시 정답으로 간주합니다. 즉, 가능한 경로가 여러 가지인 경우 모두 정답으로 인정됩니다. 경로 여러개 출력하지 말고 하나만 출력하세요.
