# GoogleTest compatibility changes

The fused GoogleTest sources retain C++11 support. The following corrections
are backported from GoogleTest release 1.12.1 without changing the test API:

- Initialize `MatcherBase`'s vtable and buffer in every constructing path.
  Empty matchers can then be copied without reading uninitialized storage.
- Represent a mock's call-reaction registration key as `uintptr_t`, consistently
  through registration, lookup, and removal. Registration records the object's
  address; it does not inspect an object whose construction has not finished.

Reference sources:

- https://github.com/google/googletest/blob/release-1.12.1/googletest/include/gtest/gtest-matchers.h
- https://github.com/google/googletest/blob/release-1.12.1/googlemock/include/gmock/gmock-nice-strict.h
- https://github.com/google/googletest/blob/release-1.12.1/googlemock/include/gmock/gmock-spec-builders.h
- https://github.com/google/googletest/blob/release-1.12.1/googlemock/src/gmock-spec-builders.cc
