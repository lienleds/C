# Unit Testing in C

Unit testing is a software testing technique where individual units or components of a program are tested in isolation to ensure they work as expected. In C, unit testing is typically performed using frameworks or custom test harnesses.

## Why Unit Testing?
- **Bug Detection**: Identify issues early in the development process.
- **Code Quality**: Ensure that code changes do not introduce new bugs.
- **Refactoring Confidence**: Safely refactor code with tests in place.
- **Documentation**: Tests serve as documentation for expected behavior.

## Popular Unit Testing Frameworks for C

### 1. **CUnit**
- **Description**: A lightweight and simple unit testing framework for C.
- **Installation**:
  ```bash
  sudo apt-get install libcunit1-dev  # On Linux
  brew install cunit                 # On macOS
  ```
- **Usage**:
  ```c
  #include <CUnit/CUnit.h>
  #include <CUnit/Basic.h>

  void test_example() {
      CU_ASSERT(2 + 2 == 4);
  }

  int main() {
      CU_initialize_registry();
      CU_pSuite suite = CU_add_suite("Example Suite", 0, 0);
      CU_add_test(suite, "Example Test", test_example);
      CU_basic_run_tests();
      CU_cleanup_registry();
      return 0;
  }
  ```

### 2. **Unity**
- **Description**: A small, portable, and flexible unit testing framework.
- **Installation**: Clone the repository from [Unity GitHub](https://github.com/ThrowTheSwitch/Unity).
- **Usage**:
  ```c
  #include "unity.h"

  void setUp() {}
  void tearDown() {}

  void test_example() {
      TEST_ASSERT_EQUAL(4, 2 + 2);
  }

  int main() {
      UNITY_BEGIN();
      RUN_TEST(test_example);
      return UNITY_END();
  }
  ```

### 3. **Check**
- **Description**: A unit testing framework with support for fixtures and mocking.
- **Installation**:
  ```bash
  sudo apt-get install check  # On Linux
  brew install check          # On macOS
  ```
- **Usage**:
  ```c
  #include <check.h>

  START_TEST(test_example) {
      ck_assert_int_eq(2 + 2, 4);
  }
  END_TEST

  Suite *example_suite() {
      Suite *s = suite_create("Example Suite");
      TCase *tc = tcase_create("Core");
      tcase_add_test(tc, test_example);
      suite_add_tcase(s, tc);
      return s;
  }

  int main() {
      Suite *s = example_suite();
      SRunner *sr = srunner_create(s);
      srunner_run_all(sr, CK_NORMAL);
      srunner_free(sr);
      return 0;
  }
  ```

### 4. **Google Test (gtest)**
- **Description**: A popular C++ testing framework that can also be used for C projects.
- **Features**: Rich assertions, parameterized tests, and mocking support.
- **Installation**: Clone the repository from [Google Test GitHub](https://github.com/google/googletest).

### 5. **Criterion**
- **Description**: A modern C unit testing framework with automatic test discovery.
- **Features**: Rich output, parallel test execution, and no boilerplate code.
- **Installation**: Clone the repository from [Criterion GitHub](https://github.com/Snaipe/Criterion).

### 6. **MinUnit**
- **Description**: A minimalistic unit testing framework for C.
- **Features**: Extremely lightweight, with only a few lines of code.
- **Website**: [MinUnit](http://www.jera.com/techinfo/jtns/jtn002.html)

### 7. **CuTest**
- **Description**: A lightweight and portable unit testing framework.
- **Features**: Simple API, small footprint, and easy integration.
- **Website**: [CuTest](http://cutest.sourceforge.net/)

### 8. **Boost.Test**
- **Description**: Part of the Boost C++ Libraries, but can be used for C projects.
- **Features**: Rich assertions, test organization, and CI integration.
- **Website**: [Boost.Test](https://www.boost.org/doc/libs/release/libs/test/)

### 9. **ZTest**
- **Description**: A lightweight testing framework for embedded systems.
- **Features**: Designed for resource-constrained environments.
- **GitHub**: [ZTest GitHub](https://github.com/zephyrproject-rtos/zephyr)

### 10. **AceUnit**
- **Description**: Advanced C and Embedded Unit Testing framework.
- **Features**: Designed for embedded systems with minimal overhead.
- **Website**: [AceUnit](http://www.xwisp.de/AceUnit/)

## Best Practices
- Write tests for all critical code paths.
- Use descriptive names for test cases.
- Run tests frequently during development.
- Integrate unit tests into your CI/CD pipeline.
- Mock external dependencies to isolate the unit under test.

## Integration with CI/CD
Unit testing frameworks can be integrated into CI/CD pipelines using tools like Jenkins, GitHub Actions, or GitLab CI. Automate test execution to ensure code quality.

## Additional Resources
- [CUnit Documentation](http://cunit.sourceforge.net/)
- [Unity GitHub Repository](https://github.com/ThrowTheSwitch/Unity)
- [Check Documentation](https://libcheck.github.io/check/)
- [Google Test GitHub](https://github.com/google/googletest)
- [Criterion GitHub](https://github.com/Snaipe/Criterion)
- [Unit Testing Best Practices](https://martinfowler.com/articles/practical-test-pyramid.html)