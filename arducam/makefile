# 헤더(.h) -> 소스(cpp) -> 목적파일 (.o) -> app
#이 구조를 스크립트로 간단하게 작성할 수 있다. = makefile


CC = g++		# CC : 컴파일러 선언
CXXFLAGS = -Wall -O2	#컴파일러 옵션
TARGET = ArduCAM

# $@ : 타겟 이름
# $< : 의존성에 첫번째 파일 이름
# $^ : 의존성 전체
# $* : 확장자(.h, .o, .cpp)를 제외한 의존성 이름 목록
INCLUDE = -Iinclude

SRC_DIR = ./src
OBJ_DIR = ./obj

SRCS =$(notdir $(wildcard $(SRC_DIR)/*.cpp)) # notdir :  경로를 제외한 파일 이름 목록만
OBJS = $(patsubst %.o, $(OBJ_DIR)/%.o,$(SRCS:.cpp=.o)) 	# patsubst(1,2,3): 변수에서 특정 패턴을 다른 문자열로 치환
														# 1,2. `.o` 의 모든 문자열을 $(OBJ_DIR)/%.o로 치환 
														# 3. 그 리스트
DEPS = $(OBJS:.o = .d)									# .d : 의존성 정보 파일 확장자로 변경

all : $(TARGET)

#SRCS = $(wildcard *.cpp)  # 와일드카드 : *.cpp의 모든 파일을 찾아 목록 반환
#OBJS = $(SRCS:.cpp=.o)	# 위 SRCS의 목록에서 .cpp를 .o로 이름 변경



# 목적 파일 만들기( 헤더 불일치( 타겟 파일 헤더 없을 때))
$(OBJ_DIR)/%.o : $(SRC_DIR)/%.cpp
	$(CC) -o $@ $(INCLUDE) $(CXXFLAGS) -c $< -MD

# 실행파일
$(TARGET): $(OBJS)
	$(CC) $(CXXFLAGS) $(OBJS) -o $(TARGET) 

.PHONY: clean all

clean:

	rm -f $(OBJS) $(DEPS) $(TARGET)

-include $(DEPS)
