---
title: dotnet-counters - .NET Core
description: dotnet-counter 명령줄 도구를 설치하고 사용하는 방법에 대해 알아봅니다.
ms.date: 02/26/2020
ms.openlocfilehash: 6a4fd92540dbc16173dfa3a10ff9dfaa1f31f7d0
ms.sourcegitcommit: 7476c20d2f911a834a00b8a7f5e8926bae6804d9
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/11/2020
ms.locfileid: "88062901"
---
# <a name="dotnet-counters"></a>dotnet-counters

**이 문서의 적용 대상:**  ✔️ .NET Core 3.0 SDK 이상 버전

## <a name="install-dotnet-counters"></a>dotnet-counters 설치

`dotnet-counters` [NuGet 패키지](https://www.nuget.org/packages/dotnet-counters)의 최신 릴리스 버전을 설치하려면 [dotnet tool install](../tools/dotnet-tool-install.md) 명령을 사용합니다.

```dotnetcli
dotnet tool install --global dotnet-counters
```

## <a name="synopsis"></a>개요

```console
dotnet-counters [-h|--help] [--version] <command>
```

## <a name="description"></a>설명

`dotnet-counters`는 임시 상태 모니터링 및 1단계 수준 성능 조사를 위한 성능 모니터링 도구입니다. <xref:System.Diagnostics.Tracing.EventCounter> API를 통해 게시된 성능 카운터 값을 관찰할 수 있습니다. 예를 들어, `PerfView` 또는 `dotnet-trace`를 사용하여 보다 심각한 성능 조사를 살펴보기 전에 의심스러운 내용이 있는지 확인하기 위해 .NET Core 애플리케이션에서 throw되는 CPU 사용량 또는 예외 비율과 같은 항목을 신속하게 모니터링할 수 있습니다.

## <a name="options"></a>옵션

- **`--version`**

  dotnet-counters 유틸리티의 버전을 표시합니다.

- **`-h|--help`**

  명령줄 도움말을 표시합니다.

## <a name="commands"></a>명령

| 명령                                             |
|-----------------------------------------------------|
| [dotnet-counters collect](#dotnet-counters-collect) |
| [dotnet-counters 목록](#dotnet-counters-list)       |
| [dotnet-counters 모니터](#dotnet-counters-monitor) |
| [dotnet-counters ps](#dotnet-counters-ps)           |

## <a name="dotnet-counters-collect"></a>dotnet-counters collect

선택한 카운터 값을 주기적으로 수집하고 후처리를 위해 지정된 파일 형식으로 내보냅니다.

### <a name="synopsis"></a>개요

```console
dotnet-counters collect [-h|--help] [-p|--process-id] [--refreshInterval] [counter_list] [--format] [-o|--output]
```

### <a name="options"></a>옵션

- **`-p|--process-id <PID>`**

  모니터링할 프로세스의 ID입니다.

- **`--refresh-interval <SECONDS>`**

  표시된 카운터 업데이트 사이의 지연 시간(초)입니다.

- **`counter_list <COUNTERS>`**

  공백으로 구분된 카운터의 목록입니다. 카운터는 `provider_name[:counter_name]`을 지정할 수 있습니다. 한정된 `counter_name` 없이 `provider_name`을 사용하면 모든 카운터가 표시됩니다. 공급자 및 카운터 이름을 검색하려면 [dotnet-counters 목록](#dotnet-counters-list) 명령을 사용합니다.

- **`--format <csv|json>`**

  내보낼 형식입니다. 현재 csv와 json을 사용할 수 있습니다.

- **`-o|--output <output>`**

  출력 파일의 이름입니다.

### <a name="examples"></a>예

- 3초의 새로 고침 간격으로 모든 카운터를 수집하고 csv를 출력으로 생성합니다.

  ```console
  > dotnet-counters collect --process-id 1902 --refresh-interval 3 --format csv

  counter_list is unspecified. Monitoring all counters by default.
  Starting a counter session. Press Q to quit.
  ```

## <a name="dotnet-counters-list"></a>dotnet-counters 목록

공급자별로 그룹화된 카운터 이름 및 설명 목록을 표시합니다.

### <a name="synopsis"></a>개요

```console
dotnet-counters list [-h|--help]
```

### <a name="example"></a>예제

```console
> dotnet-counters list
Showing well-known counters only. Specific processes may support additional counters.

System.Runtime
    cpu-usage                                    Amount of time the process has utilized the CPU (ms)
    working-set                                  Amount of working set used by the process (MB)
    gc-heap-size                                 Total heap size reported by the GC (MB)
    gen-0-gc-count                               Number of Gen 0 GCs / min
    gen-1-gc-count                               Number of Gen 1 GCs / min
    gen-2-gc-count                               Number of Gen 2 GCs / min
    time-in-gc                                   % time in GC since the last GC
    gen-0-size                                   Gen 0 Heap Size
    gen-1-size                                   Gen 1 Heap Size
    gen-2-size                                   Gen 2 Heap Size
    loh-size                                     LOH Heap Size
    alloc-rate                                   Allocation Rate
    assembly-count                               Number of Assemblies Loaded
    exception-count                              Number of Exceptions / sec
    threadpool-thread-count                      Number of ThreadPool Threads
    monitor-lock-contention-count                Monitor Lock Contention Count
    threadpool-queue-length                      ThreadPool Work Items Queue Length
    threadpool-completed-items-count             ThreadPool Completed Work Items Count
    active-timer-count                           Active Timers Count

Microsoft.AspNetCore.Hosting
    requests-per-second                  Request rate
    total-requests                       Total number of requests
    current-requests                     Current number of requests
    failed-requests                      Failed number of requests
```

> [!NOTE]
> 이러한 카운터를 지원하는 프로세스를 식별한 경우, 예를 들어 호스트 머신에서 ASP.NET Core 애플리케이션이 실행되고 있는 경우 `Microsoft.AspNetCore.Hosting` 카운터가 표시됩니다.

## <a name="dotnet-counters-monitor"></a>dotnet-counters 모니터

선택한 카운터의 값을 주기적으로 새로 고치는 방법을 표시합니다.

### <a name="synopsis"></a>개요

```console
dotnet-counters monitor [-h|--help] [-p|--process-id] [--refreshInterval] [counter_list]
```

### <a name="options"></a>옵션

- **`-p|--process-id <PID>`**

  모니터링할 프로세스의 ID입니다.

- **`--refresh-interval <SECONDS>`**

  표시된 카운터 업데이트 사이의 지연 시간(초)입니다.

- **`counter_list <COUNTERS>`**

  공백으로 구분된 카운터의 목록입니다. 카운터는 `provider_name[:counter_name]`을 지정할 수 있습니다. 한정된 `counter_name` 없이 `provider_name`을 사용하면 모든 카운터가 표시됩니다. 공급자 및 카운터 이름을 검색하려면 [dotnet-counters 목록](#dotnet-counters-list) 명령을 사용합니다.

### <a name="examples"></a>예

- 3초의 새로 고침 간격으로 `System.Runtime`의 모든 카운터를 모니터링합니다.

  ```console
  > dotnet-counters monitor --process-id 1902  --refresh-interval 3 System.Runtime

  Press p to pause, r to resume, q to quit.
    System.Runtime:
      CPU Usage (%)                                 24
      Working Set (MB)                            1982
      GC Heap Size (MB)                            811
      Gen 0 GC / second                             20
      Gen 1 GC / second                              4
      Gen 2 GC / second                              1
      Number of Exceptions / sec                     4
  ```

- `System.Runtime`에서 CPU 사용량 및 GC 힙 크기만 모니터링합니다.

  ```console
  > dotnet-counters monitor --process-id 1902 System.Runtime[cpu-usage,gc-heap-size]

  Press p to pause, r to resume, q to quit.
    System.Runtime:
      CPU Usage (%)                                 24
      GC Heap Size (MB)                            811
  ```

- 사용자 정의 `EventSource`에서 `EventCounter` 값을 모니터링합니다. 자세한 내용은 [자습서: .NET Core에서 EventCounters를 사용하여 성능 측정](event-counter-perf.md)을 참조하세요.

  ```console
  > dotnet-counters monitor --process-id 1902 Samples-EventCounterDemos-Minimal

  Press p to pause, r to resume, q to quit.
      request                                      100
  ```
  
## <a name="dotnet-counters-ps"></a>dotnet-counters ps

모니터링할 수 있는 dotnet 프로세스의 목록을 표시합니다.

### <a name="synopsis"></a>개요

```console
dotnet-counters ps [-h|--help]
```

### <a name="example"></a>예제

```console
> dotnet-counters ps
  
  15683 WebApi     /home/suwhang/repos/WebApi/WebApi
  16324 dotnet     /usr/local/share/dotnet/dotnet
```
