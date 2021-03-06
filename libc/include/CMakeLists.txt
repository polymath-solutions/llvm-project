
add_header(
  llvm_libc_common_h
  HDR
    __llvm-libc-common.h
)

add_header(
  libc_posix_types_h
  HDR
    __posix-types.h
)

add_header(
  ctype_h
  HDR
   ctype.h
  DEPENDS
    llvm_libc_common_h
)

add_gen_header(
  math_h
  DEF_FILE math.h.def
  GEN_HDR math.h
  DEPENDS
    llvm_libc_common_h
)

add_gen_header(
  assert_h
  DEF_FILE assert.h.def
  GEN_HDR assert.h
  DEPENDS
    llvm_libc_common_h
)

add_gen_header(
  string_h
  DEF_FILE string.h.def
  GEN_HDR string.h
  DEPENDS
    llvm_libc_common_h
)

add_gen_header(
  threads_h
  DEF_FILE threads.h.def
  GEN_HDR threads.h
  PARAMS
    platform_threads=../config/${LIBC_TARGET_OS}/threads.h.in
  DEPENDS
    llvm_libc_common_h
  DATA_FILES
    ../config/${LIBC_TARGET_OS}/threads.h.in
)

add_gen_header(
  errno_h
  DEF_FILE errno.h.def
  PARAMS
    platform_errno=../config/${LIBC_TARGET_OS}/errno.h.in
  GEN_HDR errno.h
  DATA_FILES
    ../config/${LIBC_TARGET_OS}/errno.h.in
)

add_gen_header(
  signal_h
  DEF_FILE signal.h.def
  PARAMS
    platform_signal=../config/${LIBC_TARGET_OS}/signal.h.in
  GEN_HDR signal.h
  DATA_FILES
    ../config/${LIBC_TARGET_OS}/signal.h.in
)

add_gen_header(
  stdlib_h
  DEF_FILE stdlib.h.def
  GEN_HDR stdlib.h
  DEPENDS
    llvm_libc_common_h
)

# TODO: Not all platforms will have a include/sys directory. Add the sys
# directory and the targets for sys/*.h files conditional to the OS requiring
# them.
file(MAKE_DIRECTORY "sys")

add_gen_header(
  sys_mman_h
  DEF_FILE sys/mman.h.def
  GEN_HDR sys/mman.h
  DEPENDS
    libc_posix_types_h
    llvm_libc_common_h
)

add_gen_header(
  sys_syscall_h
  DEF_FILE sys/syscall.h.def
  GEN_HDR sys/syscall.h
  PARAMS
    syscall_numbers=../config/${LIBC_TARGET_OS}/syscall_numbers.h.inc
  DATA_FILES
    ../config/${LIBC_TARGET_OS}/syscall_numbers.h.inc
)
