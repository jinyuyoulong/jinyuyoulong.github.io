---
title: "Swiftc"
date: 2023-03-14T22:49:45+08:00
draft: true
toc: true
images:
tags: 
  - Swift
---
Swift语言编译架构图


swiftc 终端命令

```
编译成可执行文件
 swiftc -o main.out main.swift
 
 执行
 ./main.out
 
 生成抽象语法树
 swiftc main.swift -dump-ast
 
  生成Swift中间语言
 swiftc main.swift -emit-sil
 
 查看 LLVM IR 中间表示层
 swiftc main.swift -emit-ir

 生成汇编语言
 swiftc main.swift -emit-assembly
```
示例代码
```swift
func addNum(num1:Int, num2:Int) -> Int {
    return num1 + num2
}
let sum = addNum(num1: 1, num2: 2)
print(sum)
```
ast结果
```
(source_file "main.swift"
  (func_decl range=[main.swift:1:1 - line:3:1] "addNum(num1:num2:)" interface type='(Int, Int) -> Int' access=internal
    (parameter_list range=[main.swift:1:12 - line:1:31]
      (parameter "num1" apiName=num1 type='Int' interface type='Int')
      (parameter "num2" apiName=num2 type='Int' interface type='Int'))
    (result
      (type_ident
        (component id='Int' bind=Swift.(file).Int)))
    (brace_stmt range=[main.swift:1:40 - line:3:1]
      (return_stmt range=[main.swift:2:5 - line:2:19]
        (binary_expr type='Int' location=main.swift:2:17 range=[main.swift:2:12 - line:2:19] nothrow
          (dot_syntax_call_expr implicit type='(Int, Int) -> Int' location=main.swift:2:17 range=[main.swift:2:17 - line:2:17] nothrow
            (declref_expr type='(Int.Type) -> (Int, Int) -> Int' location=main.swift:2:17 range=[main.swift:2:17 - line:2:17] decl=Swift.(file).Int extension.+ function_ref=single)
            (argument_list implicit
              (argument
                (type_expr implicit type='Int.Type' location=main.swift:2:17 range=[main.swift:2:17 - line:2:17] typerepr='Int'))
            ))
          (argument_list implicit
            (argument
              (declref_expr type='Int' location=main.swift:2:12 range=[main.swift:2:12 - line:2:12] decl=main.(file).addNum(num1:num2:).num1@main.swift:1:13 function_ref=unapplied))
            (argument
              (declref_expr type='Int' location=main.swift:2:19 range=[main.swift:2:19 - line:2:19] decl=main.(file).addNum(num1:num2:).num2@main.swift:1:23 function_ref=unapplied))
          )))))
  (top_level_code_decl range=[main.swift:4:1 - line:4:34]
    (brace_stmt implicit range=[main.swift:4:1 - line:4:34]
      (pattern_binding_decl range=[main.swift:4:1 - line:4:34]
        (pattern_named type='Int' 'sum')
        Original init:
        (call_expr type='Int' location=main.swift:4:11 range=[main.swift:4:11 - line:4:34] nothrow
          (declref_expr type='(Int, Int) -> Int' location=main.swift:4:11 range=[main.swift:4:11 - line:4:11] decl=main.(file).addNum(num1:num2:)@main.swift:1:6 function_ref=single)
          (argument_list labels=num1:num2:
            (argument label=num1
              (integer_literal_expr type='Int' location=main.swift:4:24 range=[main.swift:4:24 - line:4:24] value=1 builtin_initializer=Swift.(file).Int.init(_builtinIntegerLiteral:) initializer=**NULL**))
            (argument label=num2
              (integer_literal_expr type='Int' location=main.swift:4:33 range=[main.swift:4:33 - line:4:33] value=2 builtin_initializer=Swift.(file).Int.init(_builtinIntegerLiteral:) initializer=**NULL**))
          ))
        Processed init:
        (call_expr type='Int' location=main.swift:4:11 range=[main.swift:4:11 - line:4:34] nothrow
          (declref_expr type='(Int, Int) -> Int' location=main.swift:4:11 range=[main.swift:4:11 - line:4:11] decl=main.(file).addNum(num1:num2:)@main.swift:1:6 function_ref=single)
          (argument_list labels=num1:num2:
            (argument label=num1
              (integer_literal_expr type='Int' location=main.swift:4:24 range=[main.swift:4:24 - line:4:24] value=1 builtin_initializer=Swift.(file).Int.init(_builtinIntegerLiteral:) initializer=**NULL**))
            (argument label=num2
              (integer_literal_expr type='Int' location=main.swift:4:33 range=[main.swift:4:33 - line:4:33] value=2 builtin_initializer=Swift.(file).Int.init(_builtinIntegerLiteral:) initializer=**NULL**))
          )))
))
  (var_decl range=[main.swift:4:5 - line:4:5] "sum" type='Int' interface type='Int' access=internal let readImpl=stored immutable)
  (top_level_code_decl range=[main.swift:5:1 - line:5:10]
    (brace_stmt implicit range=[main.swift:5:1 - line:5:10]
      (call_expr type='()' location=main.swift:5:1 range=[main.swift:5:1 - line:5:10] nothrow
        (declref_expr type='(Any..., String, String) -> ()' location=main.swift:5:1 range=[main.swift:5:1 - line:5:1] decl=Swift.(file).print(_:separator:terminator:) function_ref=single)
        (argument_list labels=_:separator:terminator:
          (argument
            (vararg_expansion_expr implicit type='Any...' location=main.swift:5:7 range=[main.swift:5:7 - line:5:7]
              (array_expr implicit type='Any...' location=main.swift:5:7 range=[main.swift:5:7 - line:5:7] initializer=**NULL**
                (erasure_expr implicit type='Any' location=main.swift:5:7 range=[main.swift:5:7 - line:5:7]
                  (declref_expr type='Int' location=main.swift:5:7 range=[main.swift:5:7 - line:5:7] decl=main.(file).sum@main.swift:4:5 function_ref=unapplied)))))
          (argument label=separator
            (default_argument_expr implicit type='String' location=main.swift:5:6 range=[main.swift:5:6 - line:5:6] default_args_owner=Swift.(file).print(_:separator:terminator:) param=1))
          (argument label=terminator
            (default_argument_expr implicit type='String' location=main.swift:5:6 range=[main.swift:5:6 - line:5:6] default_args_owner=Swift.(file).print(_:separator:terminator:) param=2))
        )))))
```
swift 中间语言结果
```
sil_stage canonical

import Builtin
import Swift
import SwiftShims

func addNum(num1: Int, num2: Int) -> Int

@_hasStorage @_hasInitialValue let sum: Int { get }

// sum
sil_global hidden [let] @$s4main3sumSivp : $Int

// main
sil @main : $@convention(c) (Int32, UnsafeMutablePointer<Optional<UnsafeMutablePointer<Int8>>>) -> Int32 {
bb0(%0 : $Int32, %1 : $UnsafeMutablePointer<Optional<UnsafeMutablePointer<Int8>>>):
  alloc_global @$s4main3sumSivp                   // id: %2
  %3 = global_addr @$s4main3sumSivp : $*Int       // users: %17, %10
  %4 = integer_literal $Builtin.Int64, 1          // user: %5
  %5 = struct $Int (%4 : $Builtin.Int64)          // user: %9
  %6 = integer_literal $Builtin.Int64, 2          // user: %7
  %7 = struct $Int (%6 : $Builtin.Int64)          // user: %9
  // function_ref addNum(num1:num2:)
  %8 = function_ref @$s4main6addNum4num14num2S2i_SitF : $@convention(thin) (Int, Int) -> Int // user: %9
  %9 = apply %8(%5, %7) : $@convention(thin) (Int, Int) -> Int // user: %10
  store %9 to %3 : $*Int                          // id: %10
  %11 = integer_literal $Builtin.Word, 1          // user: %13
  // function_ref _allocateUninitializedArray<A>(_:)
  %12 = function_ref @$ss27_allocateUninitializedArrayySayxG_BptBwlF : $@convention(thin) <τ_0_0> (Builtin.Word) -> (@owned Array<τ_0_0>, Builtin.RawPointer) // user: %13
  %13 = apply %12<Any>(%11) : $@convention(thin) <τ_0_0> (Builtin.Word) -> (@owned Array<τ_0_0>, Builtin.RawPointer) // users: %15, %14
  %14 = tuple_extract %13 : $(Array<Any>, Builtin.RawPointer), 0 // user: %21
  %15 = tuple_extract %13 : $(Array<Any>, Builtin.RawPointer), 1 // user: %16
  %16 = pointer_to_address %15 : $Builtin.RawPointer to [strict] $*Any // user: %18
  %17 = load %3 : $*Int                           // user: %19
  %18 = init_existential_addr %16 : $*Any, $Int   // user: %19
  store %17 to %18 : $*Int                        // id: %19
  // function_ref _finalizeUninitializedArray<A>(_:)
  %20 = function_ref @$ss27_finalizeUninitializedArrayySayxGABnlF : $@convention(thin) <τ_0_0> (@owned Array<τ_0_0>) -> @owned Array<τ_0_0> // user: %21
  %21 = apply %20<Any>(%14) : $@convention(thin) <τ_0_0> (@owned Array<τ_0_0>) -> @owned Array<τ_0_0> // users: %30, %27
  // function_ref default argument 1 of print(_:separator:terminator:)
  %22 = function_ref @$ss5print_9separator10terminatoryypd_S2StFfA0_ : $@convention(thin) () -> @owned String // user: %23
  %23 = apply %22() : $@convention(thin) () -> @owned String // users: %29, %27
  // function_ref default argument 2 of print(_:separator:terminator:)
  %24 = function_ref @$ss5print_9separator10terminatoryypd_S2StFfA1_ : $@convention(thin) () -> @owned String // user: %25
  %25 = apply %24() : $@convention(thin) () -> @owned String // users: %28, %27
  // function_ref print(_:separator:terminator:)
  %26 = function_ref @$ss5print_9separator10terminatoryypd_S2StF : $@convention(thin) (@guaranteed Array<Any>, @guaranteed String, @guaranteed String) -> () // user: %27
  %27 = apply %26(%21, %23, %25) : $@convention(thin) (@guaranteed Array<Any>, @guaranteed String, @guaranteed String) -> ()
  release_value %25 : $String                     // id: %28
  release_value %23 : $String                     // id: %29
  release_value %21 : $Array<Any>                 // id: %30
  %31 = integer_literal $Builtin.Int32, 0         // user: %32
  %32 = struct $Int32 (%31 : $Builtin.Int32)      // user: %33
  return %32 : $Int32                             // id: %33
} // end sil function 'main'

// addNum(num1:num2:)
sil hidden @$s4main6addNum4num14num2S2i_SitF : $@convention(thin) (Int, Int) -> Int {
// %0 "num1"                                      // users: %4, %2
// %1 "num2"                                      // users: %5, %3
bb0(%0 : $Int, %1 : $Int):
  debug_value %0 : $Int, let, name "num1", argno 1 // id: %2
  debug_value %1 : $Int, let, name "num2", argno 2 // id: %3
  %4 = struct_extract %0 : $Int, #Int._value      // user: %7
  %5 = struct_extract %1 : $Int, #Int._value      // user: %7
  %6 = integer_literal $Builtin.Int1, -1          // user: %7
  %7 = builtin "sadd_with_overflow_Int64"(%4 : $Builtin.Int64, %5 : $Builtin.Int64, %6 : $Builtin.Int1) : $(Builtin.Int64, Builtin.Int1) // users: %9, %8
  %8 = tuple_extract %7 : $(Builtin.Int64, Builtin.Int1), 0 // user: %11
  %9 = tuple_extract %7 : $(Builtin.Int64, Builtin.Int1), 1 // user: %10
  cond_fail %9 : $Builtin.Int1, "arithmetic overflow" // id: %10
  %11 = struct $Int (%8 : $Builtin.Int64)         // user: %12
  return %11 : $Int                               // id: %12
} // end sil function '$s4main6addNum4num14num2S2i_SitF'

// static Int.+ infix(_:_:)
sil public_external [transparent] @$sSi1poiyS2i_SitFZ : $@convention(method) (Int, Int, @thin Int.Type) -> Int {
// %0                                             // user: %3
// %1                                             // user: %4
bb0(%0 : $Int, %1 : $Int, %2 : $@thin Int.Type):
  %3 = struct_extract %0 : $Int, #Int._value      // user: %6
  %4 = struct_extract %1 : $Int, #Int._value      // user: %6
  %5 = integer_literal $Builtin.Int1, -1          // user: %6
  %6 = builtin "sadd_with_overflow_Int64"(%3 : $Builtin.Int64, %4 : $Builtin.Int64, %5 : $Builtin.Int1) : $(Builtin.Int64, Builtin.Int1) // users: %8, %7
  %7 = tuple_extract %6 : $(Builtin.Int64, Builtin.Int1), 0 // user: %10
  %8 = tuple_extract %6 : $(Builtin.Int64, Builtin.Int1), 1 // user: %9
  cond_fail %8 : $Builtin.Int1, "arithmetic overflow" // id: %9
  %10 = struct $Int (%7 : $Builtin.Int64)         // user: %11
  return %10 : $Int                               // id: %11
} // end sil function '$sSi1poiyS2i_SitFZ'

// Int.init(_builtinIntegerLiteral:)
sil public_external [transparent] @$sSi22_builtinIntegerLiteralSiBI_tcfC : $@convention(method) (Builtin.IntLiteral, @thin Int.Type) -> Int {
// %0                                             // user: %2
bb0(%0 : $Builtin.IntLiteral, %1 : $@thin Int.Type):
  %2 = builtin "s_to_s_checked_trunc_IntLiteral_Int64"(%0 : $Builtin.IntLiteral) : $(Builtin.Int64, Builtin.Int1) // user: %3
  %3 = tuple_extract %2 : $(Builtin.Int64, Builtin.Int1), 0 // user: %4
  %4 = struct $Int (%3 : $Builtin.Int64)          // user: %5
  return %4 : $Int                                // id: %5
} // end sil function '$sSi22_builtinIntegerLiteralSiBI_tcfC'

// _allocateUninitializedArray<A>(_:)
sil [always_inline] [_semantics "array.uninitialized_intrinsic"] @$ss27_allocateUninitializedArrayySayxG_BptBwlF : $@convention(thin) <τ_0_0> (Builtin.Word) -> (@owned Array<τ_0_0>, Builtin.RawPointer)

// _finalizeUninitializedArray<A>(_:)
sil shared [readnone] [_semantics "array.finalize_intrinsic"] @$ss27_finalizeUninitializedArrayySayxGABnlF : $@convention(thin) <Element> (@owned Array<Element>) -> @owned Array<Element> {
// %0                                             // user: %2
bb0(%0 : $Array<Element>):
  %1 = alloc_stack $Array<Element>                // users: %6, %5, %4, %2
  store %0 to %1 : $*Array<Element>               // id: %2
  // function_ref Array._endMutation()
  %3 = function_ref @$sSa12_endMutationyyF : $@convention(method) <τ_0_0> (@inout Array<τ_0_0>) -> () // user: %4
  %4 = apply %3<Element>(%1) : $@convention(method) <τ_0_0> (@inout Array<τ_0_0>) -> ()
  %5 = load %1 : $*Array<Element>                 // user: %7
  dealloc_stack %1 : $*Array<Element>             // id: %6
  return %5 : $Array<Element>                     // id: %7
} // end sil function '$ss27_finalizeUninitializedArrayySayxGABnlF'

// default argument 1 of print(_:separator:terminator:)
sil shared @$ss5print_9separator10terminatoryypd_S2StFfA0_ : $@convention(thin) () -> @owned String {
bb0:
  %0 = string_literal utf8 " "                    // user: %5
  %1 = integer_literal $Builtin.Word, 1           // user: %5
  %2 = integer_literal $Builtin.Int1, -1          // user: %5
  %3 = metatype $@thin String.Type                // user: %5
  // function_ref String.init(_builtinStringLiteral:utf8CodeUnitCount:isASCII:)
  %4 = function_ref @$sSS21_builtinStringLiteral17utf8CodeUnitCount7isASCIISSBp_BwBi1_tcfC : $@convention(method) (Builtin.RawPointer, Builtin.Word, Builtin.Int1, @thin String.Type) -> @owned String // user: %5
  %5 = apply %4(%0, %1, %2, %3) : $@convention(method) (Builtin.RawPointer, Builtin.Word, Builtin.Int1, @thin String.Type) -> @owned String // user: %6
  return %5 : $String                             // id: %6
} // end sil function '$ss5print_9separator10terminatoryypd_S2StFfA0_'

// default argument 2 of print(_:separator:terminator:)
sil shared @$ss5print_9separator10terminatoryypd_S2StFfA1_ : $@convention(thin) () -> @owned String {
bb0:
  %0 = string_literal utf8 "\n"                   // user: %5
  %1 = integer_literal $Builtin.Word, 1           // user: %5
  %2 = integer_literal $Builtin.Int1, -1          // user: %5
  %3 = metatype $@thin String.Type                // user: %5
  // function_ref String.init(_builtinStringLiteral:utf8CodeUnitCount:isASCII:)
  %4 = function_ref @$sSS21_builtinStringLiteral17utf8CodeUnitCount7isASCIISSBp_BwBi1_tcfC : $@convention(method) (Builtin.RawPointer, Builtin.Word, Builtin.Int1, @thin String.Type) -> @owned String // user: %5
  %5 = apply %4(%0, %1, %2, %3) : $@convention(method) (Builtin.RawPointer, Builtin.Word, Builtin.Int1, @thin String.Type) -> @owned String // user: %6
  return %5 : $String                             // id: %6
} // end sil function '$ss5print_9separator10terminatoryypd_S2StFfA1_'

// print(_:separator:terminator:)
sil @$ss5print_9separator10terminatoryypd_S2StF : $@convention(thin) (@guaranteed Array<Any>, @guaranteed String, @guaranteed String) -> ()

// Array._endMutation()
sil shared [_semantics "array.end_mutation"] @$sSa12_endMutationyyF : $@convention(method) <Element> (@inout Array<Element>) -> () {
// %0                                             // users: %9, %1
bb0(%0 : $*Array<Element>):
  %1 = struct_element_addr %0 : $*Array<Element>, #Array._buffer // user: %2
  %2 = struct_element_addr %1 : $*_ArrayBuffer<Element>, #_ArrayBuffer._storage // user: %3
  %3 = struct_element_addr %2 : $*_BridgeStorage<__ContiguousArrayStorageBase>, #_BridgeStorage.rawValue // user: %4
  %4 = load %3 : $*Builtin.BridgeObject           // user: %5
  %5 = end_cow_mutation %4 : $Builtin.BridgeObject // user: %6
  %6 = struct $_BridgeStorage<__ContiguousArrayStorageBase> (%5 : $Builtin.BridgeObject) // user: %7
  %7 = struct $_ArrayBuffer<Element> (%6 : $_BridgeStorage<__ContiguousArrayStorageBase>) // user: %8
  %8 = struct $Array<Element> (%7 : $_ArrayBuffer<Element>) // user: %9
  store %8 to %0 : $*Array<Element>               // id: %9
  %10 = tuple ()                                  // user: %11
  return %10 : $()                                // id: %11
} // end sil function '$sSa12_endMutationyyF'

// String.init(_builtinStringLiteral:utf8CodeUnitCount:isASCII:)
sil [always_inline] [readonly] [_semantics "string.makeUTF8"] @$sSS21_builtinStringLiteral17utf8CodeUnitCount7isASCIISSBp_BwBi1_tcfC : $@convention(method) (Builtin.RawPointer, Builtin.Word, Builtin.Int1, @thin String.Type) -> @owned String



// Mappings from '#fileID' to '#filePath':
//   'main/main.swift' => 'main.swift'
```
IR 结果
```
; ModuleID = '<swift-imported-modules>'
source_filename = "<swift-imported-modules>"
target datalayout = "e-m:o-p270:32:32-p271:32:32-p272:64:64-i64:64-f80:128-n8:16:32:64-S128"
target triple = "x86_64-apple-macosx13.0.0"

%TSi = type <{ i64 }>
%swift.full_type = type { i8**, %swift.type }
%swift.type = type { i64 }
%swift.bridge = type opaque
%Any = type { [24 x i8], %swift.type* }
%TSa = type <{ %Ts12_ArrayBufferV }>
%Ts12_ArrayBufferV = type <{ %Ts14_BridgeStorageV }>
%Ts14_BridgeStorageV = type <{ %swift.bridge* }>
%swift.metadata_response = type { %swift.type*, i64 }

@"$s4main3sumSivp" = hidden global %TSi zeroinitializer, align 8
@"$sypN" = external global %swift.full_type
@"$sSiN" = external global %swift.type, align 8
@"\01l_entry_point" = private constant { i32 } { i32 trunc (i64 sub (i64 ptrtoint (i32 (i32, i8**)* @main to i64), i64 ptrtoint ({ i32 }* @"\01l_entry_point" to i64)) to i32) }, section "__TEXT, __swift5_entry, regular, no_dead_strip", align 4
@.str = private unnamed_addr constant [2 x i8] c"\0A\00"
@.str.1 = private unnamed_addr constant [2 x i8] c" \00"
@__swift_reflection_version = linkonce_odr hidden constant i16 3
@llvm.used = appending global [3 x i8*] [i8* bitcast (i32 (i32, i8**)* @main to i8*), i8* bitcast ({ i32 }* @"\01l_entry_point" to i8*), i8* bitcast (i16* @__swift_reflection_version to i8*)], section "llvm.metadata"

define i32 @main(i32 %0, i8** %1) #0 {
entry:
  %2 = bitcast i8** %1 to i8*
  %3 = call swiftcc i64 @"$s4main6addNum4num14num2S2i_SitF"(i64 1, i64 2)
  store i64 %3, i64* getelementptr inbounds (%TSi, %TSi* @"$s4main3sumSivp", i32 0, i32 0), align 8
  %4 = call swiftcc { %swift.bridge*, i8* } @"$ss27_allocateUninitializedArrayySayxG_BptBwlF"(i64 1, %swift.type* getelementptr inbounds (%swift.full_type, %swift.full_type* @"$sypN", i32 0, i32 1))
  %5 = extractvalue { %swift.bridge*, i8* } %4, 0
  %6 = extractvalue { %swift.bridge*, i8* } %4, 1
  %7 = bitcast i8* %6 to %Any*
  %8 = load i64, i64* getelementptr inbounds (%TSi, %TSi* @"$s4main3sumSivp", i32 0, i32 0), align 8
  %9 = getelementptr inbounds %Any, %Any* %7, i32 0, i32 1
  store %swift.type* @"$sSiN", %swift.type** %9, align 8
  %10 = getelementptr inbounds %Any, %Any* %7, i32 0, i32 0
  %11 = getelementptr inbounds %Any, %Any* %7, i32 0, i32 0
  %12 = bitcast [24 x i8]* %11 to %TSi*
  %._value = getelementptr inbounds %TSi, %TSi* %12, i32 0, i32 0
  store i64 %8, i64* %._value, align 8
  %13 = call swiftcc %swift.bridge* @"$ss27_finalizeUninitializedArrayySayxGABnlF"(%swift.bridge* %5, %swift.type* getelementptr inbounds (%swift.full_type, %swift.full_type* @"$sypN", i32 0, i32 1))
  %14 = call swiftcc { i64, %swift.bridge* } @"$ss5print_9separator10terminatoryypd_S2StFfA0_"()
  %15 = extractvalue { i64, %swift.bridge* } %14, 0
  %16 = extractvalue { i64, %swift.bridge* } %14, 1
  %17 = call swiftcc { i64, %swift.bridge* } @"$ss5print_9separator10terminatoryypd_S2StFfA1_"()
  %18 = extractvalue { i64, %swift.bridge* } %17, 0
  %19 = extractvalue { i64, %swift.bridge* } %17, 1
  call swiftcc void @"$ss5print_9separator10terminatoryypd_S2StF"(%swift.bridge* %13, i64 %15, %swift.bridge* %16, i64 %18, %swift.bridge* %19)
  call void @swift_bridgeObjectRelease(%swift.bridge* %19) #1
  call void @swift_bridgeObjectRelease(%swift.bridge* %16) #1
  call void @swift_bridgeObjectRelease(%swift.bridge* %13) #1
  ret i32 0
}

define hidden swiftcc i64 @"$s4main6addNum4num14num2S2i_SitF"(i64 %0, i64 %1) #0 {
entry:
  %num1.debug = alloca i64, align 8
  %2 = bitcast i64* %num1.debug to i8*
  call void @llvm.memset.p0i8.i64(i8* align 8 %2, i8 0, i64 8, i1 false)
  %num2.debug = alloca i64, align 8
  %3 = bitcast i64* %num2.debug to i8*
  call void @llvm.memset.p0i8.i64(i8* align 8 %3, i8 0, i64 8, i1 false)
  store i64 %0, i64* %num1.debug, align 8
  store i64 %1, i64* %num2.debug, align 8
  %4 = call { i64, i1 } @llvm.sadd.with.overflow.i64(i64 %0, i64 %1)
  %5 = extractvalue { i64, i1 } %4, 0
  %6 = extractvalue { i64, i1 } %4, 1
  %7 = call i1 @llvm.expect.i1(i1 %6, i1 false)
  br i1 %7, label %9, label %8

8:                                                ; preds = %entry
  ret i64 %5

9:                                                ; preds = %entry
  call void @llvm.trap()
  unreachable
}

declare swiftcc { %swift.bridge*, i8* } @"$ss27_allocateUninitializedArrayySayxG_BptBwlF"(i64, %swift.type*) #0

define linkonce_odr hidden swiftcc %swift.bridge* @"$ss27_finalizeUninitializedArrayySayxGABnlF"(%swift.bridge* %0, %swift.type* %Element) #0 {
entry:
  %Element1 = alloca %swift.type*, align 8
  %1 = alloca %TSa, align 8
  store %swift.type* %Element, %swift.type** %Element1, align 8
  %2 = bitcast %TSa* %1 to i8*
  call void @llvm.lifetime.start.p0i8(i64 8, i8* %2)
  %._buffer = getelementptr inbounds %TSa, %TSa* %1, i32 0, i32 0
  %._buffer._storage = getelementptr inbounds %Ts12_ArrayBufferV, %Ts12_ArrayBufferV* %._buffer, i32 0, i32 0
  %._buffer._storage.rawValue = getelementptr inbounds %Ts14_BridgeStorageV, %Ts14_BridgeStorageV* %._buffer._storage, i32 0, i32 0
  store %swift.bridge* %0, %swift.bridge** %._buffer._storage.rawValue, align 8
  %3 = call swiftcc %swift.metadata_response @"$sSaMa"(i64 0, %swift.type* %Element) #7
  %4 = extractvalue %swift.metadata_response %3, 0
  call swiftcc void @"$sSa12_endMutationyyF"(%swift.type* %4, %TSa* nocapture swiftself dereferenceable(8) %1)
  %._buffer2 = getelementptr inbounds %TSa, %TSa* %1, i32 0, i32 0
  %._buffer2._storage = getelementptr inbounds %Ts12_ArrayBufferV, %Ts12_ArrayBufferV* %._buffer2, i32 0, i32 0
  %._buffer2._storage.rawValue = getelementptr inbounds %Ts14_BridgeStorageV, %Ts14_BridgeStorageV* %._buffer2._storage, i32 0, i32 0
  %5 = load %swift.bridge*, %swift.bridge** %._buffer2._storage.rawValue, align 8
  %6 = bitcast %TSa* %1 to i8*
  call void @llvm.lifetime.end.p0i8(i64 8, i8* %6)
  ret %swift.bridge* %5
}

define linkonce_odr hidden swiftcc { i64, %swift.bridge* } @"$ss5print_9separator10terminatoryypd_S2StFfA0_"() #0 {
entry:
  %0 = call swiftcc { i64, %swift.bridge* } @"$sSS21_builtinStringLiteral17utf8CodeUnitCount7isASCIISSBp_BwBi1_tcfC"(i8* getelementptr inbounds ([2 x i8], [2 x i8]* @.str.1, i64 0, i64 0), i64 1, i1 true)
  %1 = extractvalue { i64, %swift.bridge* } %0, 0
  %2 = extractvalue { i64, %swift.bridge* } %0, 1
  %3 = insertvalue { i64, %swift.bridge* } undef, i64 %1, 0
  %4 = insertvalue { i64, %swift.bridge* } %3, %swift.bridge* %2, 1
  ret { i64, %swift.bridge* } %4
}

define linkonce_odr hidden swiftcc { i64, %swift.bridge* } @"$ss5print_9separator10terminatoryypd_S2StFfA1_"() #0 {
entry:
  %0 = call swiftcc { i64, %swift.bridge* } @"$sSS21_builtinStringLiteral17utf8CodeUnitCount7isASCIISSBp_BwBi1_tcfC"(i8* getelementptr inbounds ([2 x i8], [2 x i8]* @.str, i64 0, i64 0), i64 1, i1 true)
  %1 = extractvalue { i64, %swift.bridge* } %0, 0
  %2 = extractvalue { i64, %swift.bridge* } %0, 1
  %3 = insertvalue { i64, %swift.bridge* } undef, i64 %1, 0
  %4 = insertvalue { i64, %swift.bridge* } %3, %swift.bridge* %2, 1
  ret { i64, %swift.bridge* } %4
}

declare swiftcc void @"$ss5print_9separator10terminatoryypd_S2StF"(%swift.bridge*, i64, %swift.bridge*, i64, %swift.bridge*) #0

; Function Attrs: nounwind
declare void @swift_bridgeObjectRelease(%swift.bridge*) #1

; Function Attrs: argmemonly nofree nounwind willreturn writeonly
declare void @llvm.memset.p0i8.i64(i8* nocapture writeonly, i8, i64, i1 immarg) #2

; Function Attrs: nofree nosync nounwind readnone speculatable willreturn
declare { i64, i1 } @llvm.sadd.with.overflow.i64(i64, i64) #3

; Function Attrs: nofree nosync nounwind readnone willreturn
declare i1 @llvm.expect.i1(i1, i1) #4

; Function Attrs: cold noreturn nounwind
declare void @llvm.trap() #5

declare swiftcc { i64, %swift.bridge* } @"$sSS21_builtinStringLiteral17utf8CodeUnitCount7isASCIISSBp_BwBi1_tcfC"(i8*, i64, i1) #0

; Function Attrs: argmemonly nofree nosync nounwind willreturn
declare void @llvm.lifetime.start.p0i8(i64 immarg, i8* nocapture) #6

define linkonce_odr hidden swiftcc void @"$sSa12_endMutationyyF"(%swift.type* %"Array<Element>", %TSa* nocapture swiftself dereferenceable(8) %0) #0 {
entry:
  %._buffer = getelementptr inbounds %TSa, %TSa* %0, i32 0, i32 0
  %._buffer._storage = getelementptr inbounds %Ts12_ArrayBufferV, %Ts12_ArrayBufferV* %._buffer, i32 0, i32 0
  %._buffer._storage.rawValue = getelementptr inbounds %Ts14_BridgeStorageV, %Ts14_BridgeStorageV* %._buffer._storage, i32 0, i32 0
  %1 = load %swift.bridge*, %swift.bridge** %._buffer._storage.rawValue, align 8
  %._buffer1 = getelementptr inbounds %TSa, %TSa* %0, i32 0, i32 0
  %._buffer1._storage = getelementptr inbounds %Ts12_ArrayBufferV, %Ts12_ArrayBufferV* %._buffer1, i32 0, i32 0
  %._buffer1._storage.rawValue = getelementptr inbounds %Ts14_BridgeStorageV, %Ts14_BridgeStorageV* %._buffer1._storage, i32 0, i32 0
  store %swift.bridge* %1, %swift.bridge** %._buffer1._storage.rawValue, align 8
  ret void
}

declare swiftcc %swift.metadata_response @"$sSaMa"(i64, %swift.type*) #0

; Function Attrs: argmemonly nofree nosync nounwind willreturn
declare void @llvm.lifetime.end.p0i8(i64 immarg, i8* nocapture) #6

attributes #0 = { "frame-pointer"="all" "no-trapping-math"="true" "probe-stack"="__chkstk_darwin" "stack-protector-buffer-size"="8" "target-cpu"="penryn" "target-features"="+cx16,+cx8,+fxsr,+mmx,+sahf,+sse,+sse2,+sse3,+sse4.1,+ssse3,+x87" "tune-cpu"="generic" }
attributes #1 = { nounwind }
attributes #2 = { argmemonly nofree nounwind willreturn writeonly }
attributes #3 = { nofree nosync nounwind readnone speculatable willreturn }
attributes #4 = { nofree nosync nounwind readnone willreturn }
attributes #5 = { cold noreturn nounwind }
attributes #6 = { argmemonly nofree nosync nounwind willreturn }
attributes #7 = { nounwind readnone }

!llvm.module.flags = !{!0, !1, !2, !3, !4, !5, !6, !7, !8, !9, !10, !11}
!swift.module.flags = !{!12}
!llvm.linker.options = !{!13, !14, !15, !16, !17}

!0 = !{i32 2, !"SDK Version", [2 x i32] [i32 13, i32 1]}
!1 = !{i32 1, !"Objective-C Version", i32 2}
!2 = !{i32 1, !"Objective-C Image Info Version", i32 0}
!3 = !{i32 1, !"Objective-C Image Info Section", !"__DATA,__objc_imageinfo,regular,no_dead_strip"}
!4 = !{i32 4, !"Objective-C Garbage Collection", i32 84346624}
!5 = !{i32 1, !"Objective-C Class Properties", i32 64}
!6 = !{i32 1, !"Objective-C Enforce ClassRO Pointer Signing", i8 0}
!7 = !{i32 1, !"wchar_size", i32 4}
!8 = !{i32 7, !"PIC Level", i32 2}
!9 = !{i32 7, !"uwtable", i32 1}
!10 = !{i32 7, !"frame-pointer", i32 2}
!11 = !{i32 1, !"Swift Version", i32 7}
!12 = !{!"standard-library", i1 false}
!13 = !{!"-lswiftSwiftOnoneSupport"}
!14 = !{!"-lswiftCore"}
!15 = !{!"-lswift_Concurrency"}
!16 = !{!"-lswift_StringProcessing"}
!17 = !{!"-lobjc"}
```