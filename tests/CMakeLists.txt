add_test(NAME runs COMMAND udpchat)
set_tests_properties(runs PROPERTIES PASS_REGULAR_EXPRESSION "Hello, world!")
