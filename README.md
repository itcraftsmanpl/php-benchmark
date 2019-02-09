# PHP internals benchmark

My personal php internals benchmarks. :rocket:
You do not believe? check on your own:

To run:
```
composer install
vendor/bin/phpbench run bechmarks/__BenchmarkName__ --report=time --retry-threshold=1 
```

## Table of Contents

 * Array
    * [Check is array empty](#check-is-array-empty)
 * Math
    * [Exponential expression](#exponential-expression)
    * [Square root](#square-root)
 * Strict checking
    * [`in_array` strict mode](#in_array-strict-mode)


## Benchmark results

### Check is array empty
  
How to fast check if array is empty. Remember that `empty` can lead to confusion results (automatic cast type).

```
vendor/bin/phpbench run benchmarks/Array/EmptyArrayBench.php --report=time --retry-threshold=1

+------------------+---------+---------+--------+-------+
| subject          | mode    | mean    | rstdev | diff  |
+------------------+---------+---------+--------+-------+
| benchEmpty       | 0.027μs | 0.027μs | 0.41%  | 1.00x |
| benchCount       | 0.048μs | 0.048μs | 0.54%  | 1.75x |
| benchCountStrict | 0.051μs | 0.051μs | 0.26%  | 1.87x |
| benchComparision | 0.028μs | 0.028μs | 0.37%  | 1.01x |
+------------------+---------+---------+--------+-------+

```

### Exponential expression

`pow` function vs `**` operator. 	

```
vendor/bin/phpbench run benchmarks/Math/PowBench.php  --report=time --retry-threshold=1

+-----------------------------+---------+---------+--------+-------+
| subject                     | mode    | mean    | rstdev | diff  |
+-----------------------------+---------+---------+--------+-------+
| benchPowFunction            | 0.090μs | 0.090μs | 0.40%  | 3.60x |
| benchExponentiationOperator | 0.025μs | 0.025μs | 0.42%  | 1.00x |
+-----------------------------+---------+---------+--------+-------+
```

### Square root

`sqrt` function vs `** .5` operator

```
vendor/bin/phpbench run benchmarks/Math/SqrtBench.php  --report=time --retry-threshold=1 

+-----------------------------+---------+---------+--------+-------+
| subject                     | mode    | mean    | rstdev | diff  |
+-----------------------------+---------+---------+--------+-------+
| benchSqrtFunction           | 0.038μs | 0.038μs | 0.56%  | 1.53x |
| benchExponentiationOperator | 0.025μs | 0.025μs | 0.53%  | 1.00x |
+-----------------------------+---------+---------+--------+-------+
```

### `in_array` strict mode

Test strict mode in `in_array` function:

```
vendor/bin/phpbench run benchmarks/Strict/InArrayBench.php --report=time --retry-threshold=1

+-------------------------+---------+---------+--------+-------+
| subject                 | mode    | mean    | rstdev | diff  |
+-------------------------+---------+---------+--------+-------+
| benchInArray            | 0.053μs | 0.053μs | 0.41%  | 1.00x |
| benchInArrayMixed       | 0.094μs | 0.094μs | 0.51%  | 1.78x |
| benchInArrayStrict      | 0.066μs | 0.066μs | 0.48%  | 1.26x |
| benchInArrayStrictMixed | 0.078μs | 0.078μs | 0.41%  | 1.48x |
+-------------------------+---------+---------+--------+-------+
```
