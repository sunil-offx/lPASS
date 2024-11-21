#include <stdio.h>
#include <stdlib.h>
#include <sys/mman.h>

bool isPowerOfTwo(int n) {
  const uint8_t instructions[] = {
      0x48, 0x83, 0xFB, 0x00,   // cmp rbx, 0x0
      0x7E, 0x1B,               // jle false
      0x48, 0x89, 0xFB,         // mov rbx, rdi
      0x48, 0x83, 0xEB, 0x01,   // sub rbx, 0x1
      0x48, 0x21, 0xFB,         // and rbx, rdi
      0x48, 0x83, 0xFB, 0x00,   // cmp rbx, 0x0
      0x74, 0x03,               // je true
      0x75, 0x09,               // jne false 
      0xC3,                     // ret 

      // true: 
      0x48, 0xC7, 0xC0, 0x01, 0x00, 0x00, 0x00, // mov rax, 0x1
      0xC3,                                     // ret

      // false: 
      0x48, 0xC7, 0xC0, 0x00, 0x00, 0x00, 0x00, // mov rax, 0x0
      0xC3 // ret
  };

  const size_t instruction_len = sizeof(instructions);

  uint8_t *jit_mem = mmap(NULL, 64, PROT_READ | PROT_WRITE | PROT_EXEC,
                          MAP_PRIVATE | MAP_ANONYMOUS, -1, 0);

  for (int i = 0; i < instruction_len; i++) {
    jit_mem[i] = instructions[i];
  }

  return ((uint64_t(*)(int64_t))jit_mem)(n);
}
