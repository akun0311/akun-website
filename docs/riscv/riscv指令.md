---
title: rv64m
editLink: true
layout: doc
---








---

# U_TYPE

||用户自定义类型|func7|func3|opcode|指令效果|
|-|-|-|-|-|-|
|lui|u_lui|无|无|0110111||
|auipc|u_auipc|无|无|0010111||


# R_TYPE

||用户自定义类型|func7|func3|opcode|指令效果|
|-|-|-|-|-|-|
|add|r_alu_reg|0000000|000|0110011||
|sub|r_alu_reg|0100000|000|0110011||
|sll|r_alu_reg|0000000|001|0110011||
|slt|r_alu_reg|0000000|010|0110011||
|sltu|r_alu_reg|0000000|011|0110011||
|xor|r_alu_reg|0000000|100|0110011||
|srl|r_alu_reg|0000000|101|0110011||
|sra|r_alu_reg|0100000|101|0110011||
|or|r_alu_reg|0000000|110|0110011||
|and|r_alu_reg|0000000|111|0110011||
|||||||
|addw|r_alu_reg_w|0000000|000|0111011||
|subw|r_alu_reg_w|0100000|000|0111011||
|sllw|r_alu_reg_w|0000000|001|0111011||
|srlw|r_alu_reg_w|0000000|101|0111011||
|sraw|r_alu_reg_w|0100000|101|0111011||


# J_TYPE

||用户自定义类型|func7|func3|opcode|指令效果|
|-|-|-|-|-|-|
|jal|j_jal|无|无|1101111||


# S_type

||用户自定义类型|func7|func3|opcode|指令效果|
|-|-|-|-|-|-|
|sb|s_store|无|000|0100011||
|sh|s_store|无|001|0100011||
|sw|s_store|无|010|0100011||
|sd|s_store|无|011|0100011||


# B_type

||用户自定义类型|func7|func3|opcode|指令效果|
|-|-|-|-|-|-|
|beq|b_branch|无|000|1100011||
|bne|b_branch|无|001|1100011||
|blt|b_branch|无|100|1100011||
|bge|b_branch|无|101|1100011||
|bltu|b_branch|无|110|1100011||
|bgeu|b_branch|无|111|1100011||


# I_type

||用户自定义类型|func7|func3|opcode|指令效果|
|-|-|-|-|-|-|
|jalr|i_jalr|无|000|1100111||
|||||||
|lb|i_load|无|000|0000011||
|lh|i_load|无|001|0000011||
|lw|i_load|无|010|0000011||
|ld|i_load|无|011|0000011||
|lbu|i_load|无|100|0000011||
|lhu|i_load|无|101|0000011||
|lwu|i_load|无|110|0000011||
|||||||
|addi|i_alu_imm|无|000|0010011||
|slti|i_alu_imm|无|010|0010011  ||
|sltiu|i_alu_imm|无|011|0010011||
|xori|i_alu_imm|无|100|0010011||
|ori|i_alu_imm|无|110|0010011||
|andi|i_alu_imm|无|111|0010011||
|slli|i_alu_imm|000000|001|0010011||
|srli|i_alu_imm|000000|101|0010011||
|srai|i_alu_imm|010000|101|0010011||
|||||||
|||||||
|addiw|i_alu_imm_w|无|000|0011011||
|slliw|i_alu_imm_w|0000000|001|0011011||
|srliw|i_alu_imm_w|0000000|101|0011011||
|sraiw|i_alu_imm_w|0100000|101|0011011||
|||||||
|||||||
|csrrw|i_system|无|001|1110011||
|csrrs|i_system|无|010|1110011||
|csrrc|i_system|无|011|1110011||
|csrrwi|i_system|无|101|1110011||
|csrrsi|i_system|无|110|1110011||
|csrrci|i_system|无|111|1110011||
|ecall|i_system||000|1110011|这个指令信息写的不全|
|ebreak|i_system||000|1110011|这个指令信息写的不全|
|uret|i_system||000|1110011|这个指令信息写的不全|
|sret|i_system||000|1110011  |这个指令信息写的不全|
|mret|i_system||000|1110011|这个指令信息写的不全|
|wfi|i_system||000|1110011|这个指令信息写的不全|
|sfence.vma|i_system||000|1110011|这个指令信息写的不全|


# 暂未分类别的指令

||用户自定义类型|func7|func3|opcode|指令效果|
|-|-|-|-|-|-|
|fence|||000|0001111|这个指令信息写的不全|
|fence.i|||001|0001111|这个指令信息写的不全|



---
title: rv64m
editLink: true
layout: doc
---


## R_TYPE

||用户自定义类型|func7|func3|opcode|指令效果|
|-|-|-|-|-|-|
|mul|r_alu_reg|0000001|000|0110011||
|mulh|r_alu_reg|0000001|001|0110011||
|mulhsu|r_alu_reg|0000001|010|0110011||
|mulhu|r_alu_reg|0000001|011|0110011||
|div|r_alu_reg|0000001|100|0110011||
|divu|r_alu_reg|0000001|101|0110011||
|rem|r_alu_reg|0000001|110|0110011||
|remu|r_alu_reg|0000001|111|0110011||
|||||||
|mulw|r_alu_reg_w|0000001|000|0111011||
|divw|r_alu_reg_w|0000001|100|0111011||
|divuw|r_alu_reg_w|0000001|101|0111011||
|remw|r_alu_reg_w|0000001|110|0111011||
|remuw|r_alu_reg_w|0000001|111|0111011||


# 指令解读

1. mul,         就是默认signed * signed
2. mulh,        就是默认signed * signed
3. mulhsu,      最后结尾的su，就是表示signed * unsigned
4. mulsu，      最后结尾的是u, 就是表示unsigned * unsigned
wire [127:0]    ext_mul_result = {   signed_ext_alu_src1 *   signed_ext_alu_src2}; //默认是sign * signed
wire [127:0] su_ext_mul_result = {   signed_ext_alu_src1 * unsigned_ext_alu_src2};
wire [127:0]  u_ext_mul_result = { unsigned_ext_alu_src1 * unsigned_ext_alu_src2 };