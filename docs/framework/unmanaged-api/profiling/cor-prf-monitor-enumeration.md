---
title: COR_PRF_MONITOR 枚举
ms.date: 03/30/2017
api_name:
- COR_PRF_MONITOR
api_location:
- mscorwks.dll
api_type:
- COM
f1_keywords:
- COR_PRF_MONITOR
helpviewer_keywords:
- COR_PRF_MONITOR enumeration [.NET Framework profiling]
ms.assetid: 9294d702-b4e5-441c-a930-e63d27b86bfd
topic_type:
- apiref
ms.openlocfilehash: 2d7984ce109fb2bac5a36ab5e4c83f386de5a488
ms.sourcegitcommit: b11efd71c3d5ce3d9449c8d4345481b9f21392c6
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/29/2020
ms.locfileid: "76867095"
---
# <a name="cor_prf_monitor-enumeration"></a>COR_PRF_MONITOR 枚举
包含用于指定探查器希望订阅的行为、功能或事件的值。  
  
## <a name="syntax"></a>语法  
  
```cpp  
typedef enum {  
    COR_PRF_MONITOR_NONE                = 0x00000000,  
    COR_PRF_MONITOR_FUNCTION_UNLOADS    = 0x00000001,  
    COR_PRF_MONITOR_CLASS_LOADS         = 0x00000002,  
    COR_PRF_MONITOR_MODULE_LOADS        = 0x00000004,  
    COR_PRF_MONITOR_ASSEMBLY_LOADS      = 0x00000008,  
    COR_PRF_MONITOR_APPDOMAIN_LOADS     = 0x00000010,  
    COR_PRF_MONITOR_JIT_COMPILATION     = 0x00000020,  
    COR_PRF_MONITOR_EXCEPTIONS          = 0x00000040,  
    COR_PRF_MONITOR_GC                  = 0x00000080,  
    COR_PRF_MONITOR_OBJECT_ALLOCATED    = 0x00000100,  
    COR_PRF_MONITOR_THREADS             = 0x00000200,  
    COR_PRF_MONITOR_REMOTING            = 0x00000400,  
    COR_PRF_MONITOR_CODE_TRANSITIONS    = 0x00000800,  
    COR_PRF_MONITOR_ENTERLEAVE          = 0x00001000,  
    COR_PRF_MONITOR_CCW                 = 0x00002000,  
    COR_PRF_MONITOR_REMOTING_COOKIE     = 0x00004000 |   
                                          COR_PRF_MONITOR_REMOTING,  
    COR_PRF_MONITOR_REMOTING_ASYNC      = 0x00008000 |   
                                          COR_PRF_MONITOR_REMOTING,  
    COR_PRF_MONITOR_SUSPENDS            = 0x00010000,  
    COR_PRF_MONITOR_CACHE_SEARCHES      = 0x00020000,  
    COR_PRF_ENABLE_REJIT                = 0x00040000,  
    COR_PRF_ENABLE_INPROC_DEBUGGING     = 0x00080000,  
    COR_PRF_ENABLE_JIT_MAPS             = 0x00100000,  
    COR_PRF_DISABLE_INLINING            = 0x00200000,  
    COR_PRF_DISABLE_OPTIMIZATIONS       = 0x00400000,  
    COR_PRF_ENABLE_OBJECT_ALLOCATED     = 0x00800000,  
    COR_PRF_MONITOR_CLR_EXCEPTIONS      = 0x01000000,  
    COR_PRF_MONITOR_ALL                 = 0x0107FFFF,  
    COR_PRF_ENABLE_FUNCTION_ARGS        = 0X02000000,  
    COR_PRF_ENABLE_FUNCTION_RETVAL      = 0X04000000,  
    COR_PRF_ENABLE_FRAME_INFO           = 0X08000000,  
    COR_PRF_ENABLE_STACK_SNAPSHOT       = 0X10000000,  
    COR_PRF_USE_PROFILE_IMAGES          = 0x20000000,  
    COR_PRF_DISABLE_TRANSPARENCY_CHECKS_UNDER_FULL_TRUST  
                                        = 0x40000000,  
    COR_PRF_DISABLE_ALL_NGEN_IMAGES     = 0x80000000,  
    COR_PRF_ALL                         = 0x8FFFFFFF,  
    COR_PRF_REQUIRE_PROFILE_IMAGE       = COR_PRF_USE_PROFILE_IMAGES |   
                                          COR_PRF_MONITOR_CODE_TRANSITIONS |   
                                          COR_PRF_MONITOR_ENTERLEAVE,  
    COR_PRF_ALLOWABLE_AFTER_ATTACH      = COR_PRF_MONITOR_THREADS |  
                                          COR_PRF_MONITOR_MODULE_LOADS |  
                                          COR_PRF_MONITOR_ASSEMBLY_LOADS |  
                                          COR_PRF_MONITOR_APPDOMAIN_LOADS |  
                                          COR_PRF_ENABLE_STACK_SNAPSHOT |  
                                          COR_PRF_MONITOR_GC |  
                                          COR_PRF_MONITOR_SUSPENDS |  
                                          COR_PRF_MONITOR_CLASS_LOADS |  
                                          COR_PRF_MONITOR_JIT_COMPILATION,  
    COR_PRF_MONITOR_IMMUTABLE           = COR_PRF_MONITOR_CODE_TRANSITIONS |  
                                          COR_PRF_MONITOR_REMOTING |  
                                          COR_PRF_MONITOR_REMOTING_COOKIE |  
                                          COR_PRF_MONITOR_REMOTING_ASYNC |  
                                          COR_PRF_ENABLE_REJIT |  
                                          COR_PRF_ENABLE_INPROC_DEBUGGING |  
                                          COR_PRF_ENABLE_JIT_MAPS |  
                                          COR_PRF_DISABLE_OPTIMIZATIONS |  
                                          COR_PRF_DISABLE_INLINING |  
                                          COR_PRF_ENABLE_OBJECT_ALLOCATED |  
                                          COR_PRF_ENABLE_FUNCTION_ARGS |  
                                          COR_PRF_ENABLE_FUNCTION_RETVAL |  
                                          COR_PRF_ENABLE_FRAME_INFO |  
                                          COR_PRF_USE_PROFILE_IMAGES |  
                     COR_PRF_DISABLE_TRANSPARENCY_CHECKS_UNDER_FULL_TRUST |  
                                          COR_PRF_DISABLE_ALL_NGEN_IMAGES  
} COR_PRF_MONITOR;  
```  
  
## <a name="members"></a>Members  
 以下各节按类别列出 `COR_PRF_MONITOR` 枚举成员。 类别为：  
  
- [未设置标志](#None)  
  
- [回调标志](#Callback)  
  
- [功能-启用标志](#Feature)  
  
- [配置标志](#Config)  
  
- [复合标志](#Composite)  
  
<a name="None"></a>   
### <a name="no-flags-set"></a>未设置标志  
  
|成员|描述|  
|------------|-----------------|  
|`COR_PRF_MONITOR_NONE`|不设置任何标志。|  
  
<a name="Callback"></a>   
### <a name="callback-flags"></a>回调标志  
  
|成员|描述|  
|------------|-----------------|  
|`COR_PRF_MONITOR_ALL`|启用所有回调事件。|  
|`COR_PRF_MONITOR_APPDOMAIN_LOADS`|控制[ICorProfilerCallback](icorprofilercallback-interface.md)接口中的 `AppDomainCreation*` 和 `AppDomainShutdown*` 回调。|  
|`COR_PRF_MONITOR_ASSEMBLY_LOADS`|控制[ICorProfilerCallback](icorprofilercallback-interface.md)接口中的 `AssemblyLoad*` 和 `AssemblyUnload*` 回调。|  
|`COR_PRF_MONITOR_CACHE_SEARCHES`|控制[ICorProfilerCallback](icorprofilercallback-interface.md)接口中的 `JITCachedFunctionSearch*` 回调。<br /><br /> 此标志的行为在 .NET Framework 版本 2.0 中发生了变化。|  
|`COR_PRF_MONITOR_CCW`|控制[ICorProfilerCallback](icorprofilercallback-interface.md)接口中的 `COMClassicVTable*` 回调。|  
|`COR_PRF_MONITOR_CLASS_LOADS`|控制[ICorProfilerCallback](icorprofilercallback-interface.md)接口中的 `ClassLoad*` 和 `ClassUnload*` 回调。|  
|`COR_PRF_MONITOR_CLR_EXCEPTIONS`|控制[ICorProfilerCallback](icorprofilercallback-interface.md)接口中的 `ExceptionCLRCatcher*` 回调。|  
|`COR_PRF_MONITOR_CODE_TRANSITIONS`|控制[ICorProfilerCallback](icorprofilercallback-interface.md)接口中的[UnmanagedToManagedTransition](icorprofilercallback-unmanagedtomanagedtransition-method.md)和[ManagedToUnmanagedTransition](icorprofilercallback-managedtounmanagedtransition-method.md)回调|  
|`COR_PRF_MONITOR_ENTERLEAVE`|控制 `FunctionEnter*`、`FunctionLeave*`和 `FunctionTailCall*`[分析全局静态函数](profiling-global-static-functions.md)。|  
|`COR_PRF_MONITOR_EXCEPTIONS`|控制[ICorProfilerCallback](icorprofilercallback-interface.md)接口中的[ExceptionThrown](icorprofilercallback-exceptionthrown-method.md)回调和 `ExceptionSearch*`、`ExceptionOSHandler*`、`ExceptionUnwind*`和 `ExceptionCatcher*` 回调。|  
|`COR_PRF_MONITOR_FUNCTION_UNLOADS`|控制[ICorProfilerCallback](icorprofilercallback-interface.md)接口中的[FunctionUnloadStarted](icorprofilercallback-functionunloadstarted-method.md)回调。|  
|`COR_PRF_MONITOR_GC`|控制 `ICorProfilerCallback*` 接口中的[GarbageCollectionStarted](icorprofilercallback2-garbagecollectionstarted-method.md)、 [GarbageCollectionFinished](icorprofilercallback2-garbagecollectionfinished-method.md)、 [MovedReferences](icorprofilercallback-movedreferences-method.md)、 [MovedReferences2](icorprofilercallback4-movedreferences2-method.md)、 [SurvivingReferences](icorprofilercallback2-survivingreferences-method.md)、 [SurvivingReferences2](icorprofilercallback4-survivingreferences2-method.md) [、ObjectReferences、](icorprofilercallback-objectreferences-method.md) [ObjectsAllocatedByClass](icorprofilercallback-objectsallocatedbyclass-method.md)、 [RootReferences](icorprofilercallback-rootreferences-method.md)、 [RootReferences2](icorprofilercallback2-rootreferences2-method.md) [、HandleCreated、](icorprofilercallback2-handlecreated-method.md) [HandleDestroyed](icorprofilercallback2-handledestroyed-method.md)和[FinalizeableObjectQueued](icorprofilercallback2-finalizeableobjectqueued-method.md)回调。 分配 `COR_PRF_MONITOR_GC` 时，将关闭并发垃圾回收。|  
|`COR_PRF_MONITOR_JIT_COMPILATION`|控制[ICorProfilerCallback](icorprofilercallback-interface.md)接口中的 `JITCompilation*`、 [JITFunctionPitched](icorprofilercallback-jitfunctionpitched-method.md)和[JITInlining](icorprofilercallback-jitinlining-method.md)回调。|  
|`COR_PRF_MONITOR_MODULE_LOADS`|控制[ICorProfilerCallback](icorprofilercallback-interface.md)接口中的 `ModuleLoad*`、`ModuleUnload*`和[ModuleAttachedToAssembly](icorprofilercallback-moduleattachedtoassembly-method.md)回调。|  
|`COR_PRF_MONITOR_OBJECT_ALLOCATED`|控制[ICorProfilerCallback](icorprofilercallback-interface.md)接口中的[ObjectAllocated](icorprofilercallback-objectallocated-method.md)回调。|  
|`COR_PRF_MONITOR_REMOTING`|控制[ICorProfilerCallback](icorprofilercallback-interface.md)接口中的 `Remoting*` 回调。|  
|`COR_PRF_MONITOR_REMOTING_ASYNC`|控制 `Remoting*` 回调是否将监视异步事件。|  
|`COR_PRF_MONITOR_REMOTING_COOKIE`|控制是否向 `Remoting*` 回调传递 Cookie。|  
|`COR_PRF_MONITOR_SUSPENDS`|控制[ICorProfilerCallback](icorprofilercallback-interface.md)接口中的 `RuntimeSuspend*`、`RuntimeResume*`、 [RuntimeThreadSuspended](icorprofilercallback-runtimethreadsuspended-method.md)和[RuntimeThreadResumed](icorprofilercallback-runtimethreadresumed-method.md)回调。|  
|`COR_PRF_MONITOR_THREADS`|控制[ICorProfilerCallback](icorprofilercallback-interface.md)和[ICorProfilerCallback2](icorprofilercallback2-interface.md)接口中的[ThreadCreated](icorprofilercallback-threadcreated-method.md)、 [ThreadDestroyed](icorprofilercallback-threaddestroyed-method.md)、 [ThreadAssignedToOSThread](icorprofilercallback-threadassignedtoosthread-method.md)和[ThreadNameChanged](icorprofilercallback2-threadnamechanged-method.md)回调。|  
  
<a name="Feature"></a>   
### <a name="feature-enabling-flags"></a>功能启用标志  
  
|成员|描述|  
|------------|-----------------|  
|`COR_PRF_ENABLE_FRAME_INFO`|通过使用[FunctionEnter2](functionenter2-function.md)回调返回的 `COR_PRF_FRAME_INFO` 值调用[GetFunctionInfo2](icorprofilerinfo2-getfunctioninfo2-method.md)方法，可以为泛型函数检索确切 `ClassID`。|  
|`COR_PRF_ENABLE_FUNCTION_ARGS`|使用[FunctionEnter2](functionenter2-function.md)回调或[FunctionEnter3WithInfo](functionenter3withinfo-function.md)回调和[GetFunctionEnter3Info](icorprofilerinfo3-getfunctionenter3info-method.md)方法启用参数跟踪。|  
|`COR_PRF_ENABLE_FUNCTION_RETVAL`|启用使用[FunctionLeave2](functionleave2-function.md)回调或[FunctionLeave3WithInfo](functionleave3withinfo-function.md)回调和[GetFunctionLeave3Info](icorprofilerinfo3-getfunctionleave3info-method.md)方法跟踪返回值。|  
|`COR_PRF_ENABLE_INPROC_DEBUGGING`|已否决。<br /><br /> 不支持进程内调试。 此标志无效。|  
|`COR_PRF_ENABLE_JIT_MAPS`|已否决。<br /><br /> 允许探查器使用[GetILToNativeMapping](icorprofilerinfo-getiltonativemapping-method.md)获取 IL 到本机映射。 从 .NET Framework 2.0 开始，运行时始终跟踪从 IL 到本机代码的映射；因此，始终认为要设置此标志。|  
|`COR_PRF_ENABLE_OBJECT_ALLOCATED`|通知运行时：探查器可能需要对象分配通知。 在初始化期间必须设置此标志。 它允许探查器随后使用 `COR_PRF_MONITOR_OBJECT_ALLOCATED` 标志来接收[ObjectAllocated](icorprofilercallback-objectallocated-method.md)回调。|  
|`COR_PRF_ENABLE_REJIT`|启用对[RequestReJIT](icorprofilerinfo4-requestrejit-method.md)和[RequestRevert](icorprofilerinfo4-requestrevert-method.md)方法的调用。 探查器必须在启动时设置此标志。  如果探查器指定此标志，它还必须指定 `COR_PRF_DISABLE_ALL_NGEN_IMAGES`。|  
|`COR_PRF_ENABLE_STACK_SNAPSHOT`|启用对[DoStackSnapshot](icorprofilerinfo2-dostacksnapshot-method.md)方法的调用。|  
  
<a name="Config"></a>   
### <a name="configuration-flags"></a>配置标志  
  
|成员|描述|  
|------------|-----------------|  
|`COR_PRF_DISABLE_ALL_NGEN_IMAGES`|阻止所有本机映像（包括增强型探查器映像）进行加载。  如果此标志和 `COR_PRF_USE_PROFILE_IMAGES` 标志都已指定，将使用 `COR_PRF_DISABLE_ALL_NGEN_IMAGES`。|  
|`COR_PRF_DISABLE_INLINING`|禁用所有内联。|  
|`COR_PRF_DISABLE_OPTIMIZATIONS`|禁用所有代码优化。|  
|`COR_PRF_DISABLE_TRANSPARENCY_CHECKS_UNDER_FULL_TRUST`|禁用正常情况下在实时 (JIT) 编译和完全信任程序集类加载过程中完成的安全透明度检查。 这可以使某些检测更容易执行。|  
|`COR_PRF_USE_PROFILE_IMAGES`|导致执行本机映像搜索，以查找增强型探查器映像。 对于给定程序集，如果找不到增强型探查器映像，则公共语言运行时将回退到该程序集的 JIT。 如果此标志和 `COR_PRF_DISABLE_ALL_NGEN_IMAGES` 标志都已指定，将使用 `COR_PRF_DISABLE_ALL_NGEN_IMAGES`。|  
  
<a name="Composite"></a>   
### <a name="composite-flags"></a>复合标志  
  
|成员|描述|  
|------------|-----------------|  
|`COR_PRF_ALL`|表示所有 `COR_PRF_MONITOR` 标志值。|  
|`COR_PRF_ALLOWABLE_AFTER_ATTACH`|表示可以在将探查器附加到运行中的应用之后进行设置的所有 `COR_PRF_MONITOR` 标志。 语法部分指示此位掩码中存在的各个标志。|  
|`COR_PRF_MONITOR_ALL`|启用所有回调事件。|  
|`COR_PRF_MONITOR_IMMUTABLE`|表示只能在初始化过程中进行设置的所有 `COR_PRF_MONITOR` 标志。 如果在初始化后尝试更改这些标志中的任一标志，则会返回一个指示失败的 `HRESULT` 值。|  
|`COR_PRF_REQUIRE_PROFILE_IMAGE`|表示需要配置增强的映像的所有 `COR_PRF_MONITOR` 标志。|  
  
## <a name="remarks"></a>备注  
 `COR_PRF_MONITOR` 值与[ICorProfilerInfo：： GetEventMask](icorprofilerinfo-geteventmask-method.md)和[ICorProfilerInfo：： SetEventMask](icorprofilerinfo-seteventmask-method.md)方法一起使用，以定义公共语言运行时对探查器发出的事件通知。  
  
## <a name="requirements"></a>需求  
 **平台：** 请参阅[系统要求](../../../../docs/framework/get-started/system-requirements.md)。  
  
 **头文件：** CorProf.idl、CorProf.h  
  
 **库：** CorGuids.lib  
  
 **.NET Framework 版本：** [!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]  
  
## <a name="see-also"></a>另请参阅

- [分析枚举](profiling-enumerations.md)
- [GetEventMask 方法](icorprofilerinfo-geteventmask-method.md)
- [SetEventMask 方法](icorprofilerinfo-seteventmask-method.md)
