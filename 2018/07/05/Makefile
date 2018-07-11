all: dotproductstandard dotproduct
dotproductstandard: dotproduct.cpp benchmark.h
	c++ -O3 -std=c++17 -Wall -Wextra -Werror -o dotproductstandard dotproduct.cpp -march=native 
dotproduct: dotproduct.cpp benchmark.h
	c++ -O3 -std=c++17 -Wall -Wextra -Werror -o dotproduct dotproduct.cpp -march=native -ffast-math


test:dotproduct
	./dotproduct

clean:
	rm -r -f dotproduct dotproductstandard
