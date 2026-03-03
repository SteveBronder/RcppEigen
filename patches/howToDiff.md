
### Hint

```sh
diff --exclude=CMakeLists.txt -ruw eigen-3.4.0/Eigen/ inst/include/Eigen/ > patches/eigen-3.4.0.diff
diff --exclude=CMakeLists.txt -ruw eigen-3.4.0/unsupported/Eigen/ inst/include/unsupported/Eigen/ >> patches/eigen-3.4.0.diff
```

For Eigen 5.0.2 and later, a git-diff workflow that captures only RcppEigen local
patches from the vendor baseline can be used:

```sh
git diff --src-prefix=c/ --dst-prefix=w/ <vendor-commit>..HEAD -- \
  inst/include/Eigen/CholmodSupport \
  inst/include/Eigen/src/CholmodSupport/CholmodSupport.h \
  inst/include/Eigen/src/Core/util/DisableStupidWarnings.h \
  inst/include/unsupported/Eigen/src/SparseExtra/MatrixMarketIterator.h \
  inst/include/RcppEigenForward.h \
  inst/include/RcppEigenWrap.h \
  inst/tinytest/cpp/rcppeigen.cpp \
  inst/tinytest/cpp/sparse.cpp \
  inst/tinytest/test_sparse.R \
  src/fastLm.cpp > patches/eigen-5.0.2.diff
```
