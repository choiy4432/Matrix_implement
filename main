class Matrix:
    def __init__(self, vectors):
        assert isinstance(vectors, list), 'Input argument must be a list.'
        assert all([isinstance(vector, list) for vector in vectors]), 'Row vectors must be a list.'
        assert all(len(vector) == len(vectors[0]) for vector in vectors), 'Row vectors must have the same length.'
        self.vectors = vectors                               #입력받은 vectors를 self.vectors에 저장한다.
        self.shape = (len(vectors), len(vectors[0]))         #Matrix의 크기를 len함수를 사용하여 self.shape에 저장한다.

    
    def __str__(self):                                      #print(Matrix([[1, 2, 3], [4, 5, 6]])) 의 출력값을 지정해주기 위한 method
        le = len(self.vectors)                               #입력받은 vectors의 크기를 구해서 그 값을 le 변수에 저장해준다.
        line = ""                                            #line이라는 string을 만들어준다.
        for i in range(le):
            line += str(self.vectors[i]) + "\n "             #입력받은 vectors를 하나의 vector마다 줄바꿈을 추가하여 line에 string으로 저장한다.
        return "[" + line.rstrip("\n ") + "]"               #마지막에 불필요하게 줄바꿈이 하나 들어가있으므로 제거해준 후, []를 앞 뒤에 붙여준다.

    
    def __len__(self):                                      #len(Matrix...)를 입력하였을 때 row vector의 크기를 출력하기 위한 method
        return len(self.vectors)                           #return 값으로 len(self.vectors)를 해주면 된다.

    
    def __add__(self, other):                              #Matrix간, 그리고 Matrix와 실수의 덧셈을 출력하기 위한 method
    
        answer = []                                        #answer 라는 변수를 미리 선언
        if(isinstance(other, int)):                        #더하려는 변수가 int형인 경우(실수합)
            answer = []
            for i in range(len(self.vectors)):            #self.vectors의 길이만큼 반복
                tmp = []                                  #임시저장용 변수
                for j in range(len(self.vectors[0])):
                    tmp.append(self.vectors[i][j] + other)#더한 값을 tmp에 저장
                answer.append(tmp)                       #tmp값을 answer에 저장
        elif(isinstance(other.vectors, list)):           #더하려는 변수가 Matrix일 경우
            assert len(self.vectors) == len(other.vectors), 'Two matrixes should be the same dimension.'#에러메세지
            assert len(self.vectors[0]) == len(other.vectors[0]), 'Two matrixes should be the same dimension.'
            assert all(len(vector) == len(other.vectors[0]) for vector in other.vectors), 'Row vectors must have the same length.'
            for i in range(len(other.vectors)):        #other.vectors의 길이만큼 반복 self.vectors여도 상관없음
                tmp = []
                for j in range(len(other.vectors[i])):
                    tmp.append(self.vectors[i][j] + other.vectors[i][j]) #위와 같은 방법으로 덧셈 진행
                answer.append(tmp)
        return Matrix(answer)
    def __radd__(self, other):                         #덧셈 교환법칙
        return self.__add__(other)                     #__add__의 값을 return 해준다.

    def __mul__(self, other):                         #Matrix의 외적, 실수배를 위한 method    
        if(isinstance(other, int)):                   #입력받은 변수가 int, 실수인 경우.
            answer = [[0]*len(self.vectors[0]) for i in range(len(self.vectors))] #결과값을 저장할 list를 만들어준다.
            for i in range(len(self.vectors)):
                for j in range(len(self.vectors[i])):
                    answer[i][j] = self.vectors[i][j] * other   #행렬의 요소들을 실수배하여 list answer에 저장한다.
            return Matrix(answer)
        elif(isinstance(other, float)):               #추후의 나눗셈의 경우 역수를 활용하기 때문에 float형식도 위와 같이 만들어주었다.
            answer = [[0]*len(self.vectors[0]) for i in range(len(self.vectors))]
            for i in range(len(self.vectors)):
                for j in range(len(self.vectors[i])):
                    answer[i][j] = self.vectors[i][j] * other
            return Matrix(answer)
        elif(isinstance(other.vectors, list)):       #외적
            answer = [[0]*len(other.vectors[0]) for i in range(len(other.vectors))]#마찬가지로 답을 저장할 list를 만들어준다.
            
            assert len(self.vectors[0]) == len(other.vectors), 'Can\'t multiply.' #에러 메세지
            assert all(len(vector) == len(other.vectors[0]) for vector in other.vectors), 'Row vectors must have the same length.'
            for i in range(len(self.vectors)):
                for j in range(len(other.vectors[0])):
                    tmp = 0 #계산값을 임시로 저장할 변수를 선언
                    for k in range(len(self.vectors[0])):
                        tmp += self.vectors[i][k] * other.vectors[k][j] #계산값을 임시로 저장
                    answer[i][j] = tmp #임시로 저장한 값을 해당 list에 저장.
            return Matrix(answer)

    def __rmul__(self, other): #곱셈의 교환법칙
        return self.__mul__(other) #__mul__값을 return 해준다.

    def __neg__(self): #Matrix의 부호변환
        return (-1) * self #self에 -1을 곱해준 값을 return해준다.

    def __sub__(self, other): #Matrix의 뺄셈
        return self + (-other) #other에 -를 붙인값을 self에 더해준 값을 return 한다.

    def __rsub__(self, other): #뺄셈의 교환법칙
        return other + (-self) #__sub__와 반대 순서로 덧셈을 한다.

    def __truediv__(self, other): #Matrix의 나눗셈
        return self * (other)**(-1) #other의 역수를 self에 곱해준다.
    
    def __eq__(self, other): #두 Matrix 비교
         if(self.vectors == other.vectors): #두 요소가 동일할 경우 True를 return, 동일하지 않을 경우 False를 return
            return True
         else:
            return False

    
    def __ne__(self, other): #두 Matrix 비교
        if(self.vectors != other.vectors): #두 요소가 동일하지 않을 경우 True를 return, 동일할 경우 False를 return.
            return True
        else:
            return False
