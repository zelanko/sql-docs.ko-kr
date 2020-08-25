---
title: VDI 백업 사양 - SQL Server on Linux
description: SQL Server on Linux VDI(가상 디바이스 인터페이스) 클라이언트 SDK에서 제공하는 인터페이스에 대해 알아봅니다.
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: vanto
ms.date: 03/17/2017
ms.topic: conceptual
ms.prod: sql
ms.technology: linux
ms.assetid: 0250ba2b-8cdd-450e-9109-bf74f70e1247
ms.openlocfilehash: 1580977da984e84bd244166651330ab91665c774
ms.sourcegitcommit: 3ea082c778f6771b17d90fb597680ed334d3e0ec
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/11/2020
ms.locfileid: "88088993"
---
# <a name="sql-server-on-linux-vdi-client-sdk-specification"></a>SQL Server on Linux VDI 클라이언트 SDK 사양

[!INCLUDE [SQL Server - Linux](../includes/applies-to-version/sql-linux.md)]

이 문서에서는 SQL Server on Linux VDI(가상 디바이스 인터페이스) 클라이언트 SDK에서 제공하는 인터페이스에 대해 설명합니다. ISV(Independent Software Vendor)는 가상 백업 디바이스 API(애플리케이션 프로그래밍 인터페이스)를 사용하여 SQL Server를 해당 제품에 통합합니다. 일반적으로 Linux 기반 VDI는 Windows 기반 VDI와 비슷하게 동작하며 변경 내용은 다음과 같습니다.

- Windows 공유 메모리는 POSIX 공유 메모리가 됩니다.
- Windows 세마포는 POSIX 세마포가 됩니다.
- HRESULT 및 DWORD 같은 Windows 형식이 정수 형식으로 변경됩니다.
- COM 인터페이스는 제거되고 C++ 클래스 쌍으로 바뀝니다.
- SQL Server on Linux는 명명된 인스턴스를 지원하지 않으므로 인스턴스 이름에 대한 참조가 제거되었습니다. 
- 공유 라이브러리는/opt/mssql/lib/libsqlvdi.so에 설치된 libsqlvdi.so에서 구현됨

이 문서는 Windows MS SQL Server VDI 사양을 자세히 설명하는 **vbackup.chm**의 추록입니다. [Windows SQL VDI 사양](https://www.microsoft.com/download/details.aspx?id=17282)을 다운로드 합니다.

또한 [SQL Server 샘플 GitHub 리포지토리](https://github.com/Microsoft/sql-server-samples/tree/master/samples/features/sqlvdi-linux)에서 샘플 VDI 백업 솔루션을 검토합니다.

## <a name="user-permissions-setup"></a>사용자 권한 설정

Linux에서 POSIX 기본 형식은 기본 형식을 만드는 사용자 및 해당 기본 그룹이 소유합니다. SQL Server에서 만든 개체의 경우 이 기본 형식은 기본적으로 mssql 사용자 및 mssql 그룹이 소유합니다. SQL Server와 VDI 클라이언트 간에 공유를 허용하려면 다음 두 가지 방법 중 하나를 사용하는 것이 좋습니다.

1. mssql 사용자로 VDI 클라이언트 실행
   
   다음 명령을 실행하여 mssql 사용자로 전환합니다.
   
   ```bash
   sudo su mssql
   ```

2. mssql 사용자를 vdiuser의 그룹에 추가하고 vdiuser를 mssql 그룹에 추가합니다.
   
   다음 명령을 실행합니다.

   ```bash
   sudo useradd vdiuser
   sudo usermod -a -G mssql vdiuser
   sudo usermod -a -G vdiuser mssql
   ```

   서버를 다시 시작하여 SQL Server 및 vdiuser에 대한 새 그룹 선택

## <a name="client-functions"></a>클라이언트 함수

이 챕터에는 각 클라이언트 함수에 대한 설명이 포함되어 있습니다. 설명에는 다음 정보가 포함됩니다.

- 함수 용도
- 함수 구문
- 매개 변수 목록
- 반환 값
- 설명

## <a name="clientvirtualdevicesetcreate"></a>ClientVirtualDeviceSet::Create

**용도** 이 함수는 가상 디바이스 세트를 만듭니다.

**구문**
   ```
   int ClientVirtualDeviceSet::Create (
   char *   name,       // name for the set
   VDConfig   * cfg     // configuration for the set
   );
   ```

| 매개 변수 | 인수 | 설명
| ----- | ----- | ------ |
| | **name** | 가상 디바이스 세트를 식별합니다. CreateFileMapping()에서 사용되는 이름에 대한 규칙을 따라야 합니다. 백슬래시(\))를 제외한 모든 문자를 사용할 수 있습니다. 문자열입니다. 사용자의 제품 또는 회사 이름과 데이터베이스 이름이 포함된 문자열을 접두사로 사용하는 것이 좋습니다. |
| |**cfg** | 가상 디바이스 세트의 구성입니다. 자세한 내용은 이 문서의 뒷부분에 나오는 “구성”을 참조하세요.

| 반환 값 | 인수 | 설명
| ----- | ----- | ------ |
| |**NOERROR** | 함수가 성공했습니다. |
| |**VD_E_NOTSUPPORTED** |구성에 있는 하나 이상의 필드가 잘못되었거나 지원되지 않습니다. |
| |**VD_E_PROTOCOL** | 가상 디바이스 세트가 이미 있습니다.

**설명** Create 메서드는 BACKUP 또는 RESTORE 작업당 한 번만 호출해야 합니다. Close 메서드를 호출한 후 클라이언트는 인터페이스를 다시 사용하여 다른 가상 디바이스 세트를 만들 수 있습니다.

## <a name="clientvirtualdevicesetgetconfiguration"></a>ClientVirtualDeviceSet::GetConfiguration

**용도** 이 함수는 서버가 가상 디바이스 세트를 집합을 구성할 때까지 기다리는 데 사용됩니다.
**구문**
   ```
   int ClientVirtualDeviceSet::GetConfiguration (
   time_t       timeout,    // in milliseconds
   VDConfig *       cfg // selected configuration
   );
   ```

| 매개 변수 | 인수 | 설명
| ----- | ----- | ------ |
| | **timeout** | 시간 제한(밀리초)입니다. 시간 제한을 방지하려면 INFINITE 또는 음의 정수를 사용합니다.
| | **cfg** | 성공적으로 실행되면 서버에서 선택한 구성이 포함됩니다. 자세한 내용은 이 문서의 뒷부분에 나오는 “구성”을 참조하세요.

| 반환 값 | 인수 | 설명
| ----- | ----- | ------ |
| |**NOERROR** | 구성이 반환되었습니다.
| |**VD_E_ABORT** |SignalAbort가 호출되었습니다.
| |**VD_E_TIMEOUT** |함수 시간이 초과되었습니다.

**설명** 이 함수는 경고 가능 상태에서 차단됩니다. 성공적으로 호출된 후에는 가상 디바이스 세트의 디바이스가 열릴 수 있습니다.


## <a name="clientvirtualdevicesetopendevice"></a>ClientVirtualDeviceSet::OpenDevice
**용도** 이 함수는 가상 디바이스 세트의 디바이스 중 하나를 엽니다.
**구문**
   ```
   int ClientVirtualDeviceSet::OpenDevice (
   char *           name,       // name for the set
   ClientVirtualDevice **       ppVirtualDevice // returns interface to device
   );
   ```

| 매개 변수 | 인수 | 설명
| ----- | ----- | ------ |
| | **name** |가상 디바이스 세트를 식별합니다.
| | **ppVirtualDevice** |함수가 성공하면 가상 디바이스에 대한 포인터가 반환됩니다. 이 디바이스는 GetCommand 및 CompleteCommand에 사용됩니다.

| 반환 값 | 인수 | 설명
| ----- | ----- | ------ |
| |**NOERROR** |함수가 성공했습니다.
| |**VD_E_ABORT** | 중단이 요청되었습니다.
| |**VD_E_OPEN** |  모든 디바이스가 열립니다.
| |**VD_E_PROTOCOL** |  세트가 초기화 상태가 아니거나 이 특정 디바이스가 이미 열려 있습니다.
| |**VD_E_INVALID** |디바이스 이름이 잘못되었습니다. 세트를 구성하는 것으로 알려진 이름 중 하나가 아닙니다.

**설명** VD_E_OPEN가 문제없이 반환될 수 있습니다. 클라이언트는 이 코드가 반환될 때까지 루프를 통해 OpenDevice를 호출할 수 있습니다.
두 개 이상의 디바이스(예: *n*개 디바이스)가 구성된 경우 가상 디바이스 세트는 *n*개의 고유한 디바이스 인터페이스를 반환합니다.

`GetConfiguration` 함수는 디바이스를 열 수 있을 때까지 대기하는 데 사용될 수 있습니다.
이 함수가 실패하면 ppVirtualDevice를 통해 null 값이 반환됩니다.
 
## <a name="clientvirtualdevicegetcommand"></a>ClientVirtualDevice::GetCommand

**용도** 이 함수는 디바이스 큐에 추가된 다음 명령을 가져오는 데 사용됩니다. 요청될 때 이 함수는 다음 명령을 기다립니다.

**구문**
   ```
   int ClientVirtualDevice::GetCommand (
   time_t       timeout,    // time-out in milliseconds
   VDC_Command**    ppCmd   // returns the next command
   );
   ```

| 매개 변수 | 인수 | 설명
| ----- | ----- | ------ |
| |**timeout** |대기할 시간(밀리초)입니다. 무기한 대기하려면 INFINTE를 사용합니다. 명령을 폴링하려면 0을 사용합니다. 현재 사용할 수 있는 명령이 없으면 VD_E_TIMEOUT이 반환됩니다. 시간 초과가 발생하면 클라이언트는 다음 작업을 결정합니다.
| |**Timeout** |대기할 시간(밀리초)입니다. 무기한 대기하려면 INFINTE 또는 음수 값을 사용합니다. 명령을 폴링하려면 0을 사용합니다. 시간 제한이 만료되기 전에 사용할 수 있는 명령이 없으면 VD_E_TIMEOUT이 반환됩니다. 시간 초과가 발생하면 클라이언트는 다음 작업을 결정합니다.
| |**ppCmd** |명령이 성공적으로 반환되면 매개 변수는 실행할 명령의 주소를 반환합니다. 반환된 메모리는 읽기 전용입니다. 명령이 완료되면 이 포인터가 CompleteCommand 루틴으로 전달됩니다. 각 명령에 대한 자세한 내용은 이 문서의 뒷부분에 나오는 “명령”을 참조하세요.
        
| 반환 값 | 인수 | 설명
| ----- | ----- | ------ |
| |**NOERROR** |명령을 가져왔습니다.
| |**VD_E_CLOSE** |서버에서 디바이스를 닫았습니다.
| |**VD_E_TIMEOUT** |사용할 수 있는 명령이 없으며 시간 제한이 만료되었습니다.
| |**VD_E_ABORT** |클라이언트 또는 서버가 SignalAbort를 사용하여 강제로 종료했습니다.

**설명** VD_E_CLOSE가 반환될 때 SQL Server가 디바이스를 닫았습니다. 정상적인 종료의 일부입니다. 모든 디바이스가 닫힌 후 클라이언트는 ClientVirtualDeviceSet::Close를 호출하여 가상 디바이스 세트를 닫습니다.
명령을 기다리기 위해 이 루틴이 차단되어야 하는 경우 스레드는 경고 가능 조건으로 남아 있습니다.

## <a name="clientvirtualdevicecompletecommand"></a>ClientVirtualDevice::CompleteCommand

**용도** 이 함수는 명령이 완료되었음을 SQL Server에 알리는 데 사용됩니다. 명령에 적합한 완료 정보가 반환되어야 합니다. 자세한 내용은 이 문서의 뒷부분에 나오는 “명령”을 참조하세요.

**구문** 

   ```
   int ClientVirtualDevice::CompleteCommand (
   VDC_Command pCmd,        // the command
   int  completionCode,     // completion code
   unsigned long    bytesTransferred,   // bytes transferred
   int64_t  position        // current position
   );
   ```

| 매개 변수 | 인수 | 설명
| ----- | ----- | ------ |
| |**pCmd** |이전에 ClientVirtualDevice::GetCommand에서 반환된 명령의 주소입니다.
| |**completionCode** |완료 상태를 나타내는 상태 코드입니다. 이 매개 변수는 모든 명령에 대해 반환되어야 합니다. 반환된 코드는 실행 중인 명령에 적합해야 합니다. ERROR_SUCCESS는 모든 사례에서 성공적으로 실행된 명령을 나타내는 데 사용됩니다. 가능한 코드의 전체 목록은 vdierror.h 파일을 참조하세요. 각 명령의 일반적인 상태 코드 목록은 이 문서의 뒷부분에 나오는 “명령”에 표시됩니다.
| |**bytesTransferred** |성공적으로 전송된 바이트 수입니다. 데이터 전송 명령 Read 및 Write에 대해서만 반환됩니다.
| |**position** |GetPosition 명령에만 해당하는 응답입니다.
        
| 반환 값 | 인수 | 설명
| ----- | ----- | ------ |
| |**NOERROR** |완료가 올바르게 표시되었습니다.
| |**VD_E_INVALID** |pCmd가 활성 명령이 아닙니다.
| |**VD_E_ABORT** |중단 신호를 받았습니다.
| |**VD_E_PROTOCOL** |디바이스가 열리지 않습니다.

**설명** 없음

## <a name="clientvirtualdevicesetsignalabort"></a>ClientVirtualDeviceSet::SignalAbort

**용도** 이 함수는 비정상적인 종료가 발생해야 함을 신호로 알리는 데 사용됩니다.

**구문** 

   ```
   int ClientVirtualDeviceSet::SignalAbort ();
   ```

| 매개 변수 | 인수 | 설명
| ----- | ----- | ------ |
| |None | 해당 없음
        
| 반환 값 | 인수 | 설명
| ----- | ----- | ------ |
| |**NOERROR**|중단 알림이 게시되었습니다.

**설명** 언제든지 클라이언트는 BACKUP 또는 RESTORE 작업을 중단하도록 선택할 수 있습니다. 이 루틴은 모든 작업이 중단되어야 함을 신호로 알립니다. 전체 가상 디바이스 세트의 상태가 비정상적으로 종료된 상태로 전환됩니다. 모든 디바이스에서 추가 명령이 반환되지 않습니다. 완료되지 않은 모든 명령이 자동으로 완료되고 ERROR_OPERATION_ABORTED가 완료 코드로 반환됩니다. 클라이언트는 클라이언트에 제공된 버퍼의 처리되지 않은 사용을 안전하게 종료한 후 ClientVirtualDeviceSet::Close를 호출해야 합니다. 자세한 내용은 이 문서의 앞부분에 나오는 “비정상적인 종료”를 참조하세요.

## <a name="clientvirtualdevicesetclose"></a>ClientVirtualDeviceSet::Close

**용도** 이 함수는 ClientVirtualDeviceSet::Create에서 만든 가상 디바이스 세트를 닫습니다. 그러면 가상 디바이스 세트에 연결된 모든 리소스가 해제됩니다.

**구문** 

   ```
   int ClientVirtualDeviceSet::Close ();
   ```

| 매개 변수 | 인수 | 설명
| ----- | ----- | ------ |
| |None |해당 없음
        
| 반환 값 | 인수 | 설명
| ----- | ----- | ------ |
| |**NOERROR** |가상 디바이스 세트가 성공적으로 닫힌 경우 반환됩니다.
| |**VD_E_PROTOCOL** |가상 디바이스 세트가 열리지 않았으므로 아무 작업도 수행되지 않았습니다.
| |**VD_E_OPEN** |디바이스가 열려 있었습니다.

**설명** Close 호출은 가상 디바이스 세트에서 사용되는 모든 리소스를 해제해야 하는 클라이언트 선언입니다. 클라이언트는 Close를 호출하기 전에 데이터 버퍼 및 가상 디바이스와 관련된 모든 작업이 종료되었는지 확인해야 합니다. OpenDevice에서 반환된 모든 가상 디바이스 인터페이스는 Close로 무효화됩니다.
클라이언트는 Close 호출이 반환된 후에 가상 디바이스 세트 인터페이스에서 Create 호출을 실행할 수 있습니다. 해당 호출은 후속 BACKUP 또는 RESTORE 작업에 대한 새 가상 디바이스 세트를 만듭니다.
하나 이상의 가상 디바이스가 열려 있을 때 Close를 호출하면 VD_E_OPEN이 반환됩니다. 이 경우 가능한 경우 적절한 종료를 보장하기 위해 SignalAbort는 내부적으로 트리거됩니다. VDI 리소스가 해제됩니다. 클라이언트는 ClientVirtualDeviceSet::Close를 호출하기 전에 각 디바이스에서 VD_E_CLOSE 표시를 기다려야 합니다. 클라이언트는 가상 디바이스 세트가 이미 비정상적으로 종료된 상태임을 인식하면 GetCommand에서 VD_E_CLOSE 표시를 예상하지 않으며, 공유 버퍼의 활동이 종료되는 즉시 ClientVirtualDeviceSet::Close를 호출할 수 있습니다.
자세한 내용은 이 문서의 앞부분에 나오는 “비정상적인 종료”를 참조하세요.

## <a name="clientvirtualdevicesetopeninsecondary"></a>ClientVirtualDeviceSet::OpenInSecondary

**용도** 이 함수는 보조 클라이언트에서 가상 디바이스 세트를 엽니다. 기본 클라이언트는 이미 Create 및 GetConfiguration을 사용하여 가상 디바이스 세트를 설정했어야 합니다.

**구문** 
   
   ```
   int ClientVirtualDeviceSet::OpenInSecondary (
   char *   setName         // name of the set
   );
   ```

| 매개 변수 | 인수 | 설명
| ----- | ----- | ------ |
| |**setName** |세트를 식별합니다. 이 이름은 대/소문자를 구분하며 ClientVirtualDeviceSet::Create를 호출할 때 기본 클라이언트에서 사용하는 이름과 일치해야 합니다.

| 반환 값 | 인수 | 설명
| ----- | ----- | ------ |
| |**NOERROR** |함수가 성공했습니다.
| |**VD_E_PROTOCOL** |가상 디바이스 세트가 생성되지 않았거나, 이 클라이언트에서 이미 열려 있거나, 가상 디바이스 세트가 보조 클라이언트의 열기 요청을 수락할 준비가 되지 않았습니다.
| |**VD_E_ABORT** |작업이 중단되고 있습니다.

**설명** 다중 프로세스 모델을 사용하는 경우 기본 클라이언트는 보조 클라이언트의 정상적인 종료와 비정상적인 종료를 탐지해야 합니다.

## <a name="clientvirtualdevicesetgetbufferhandle"></a>ClientVirtualDeviceSet::GetBufferHandle

**용도** 일부 애플리케이션은 ClientVirtualDevice::GetCommand에서 반환된 버퍼에서 작동할 두 개 이상의 프로세스가 필요할 수 있습니다. 이 경우 명령을 수신하는 프로세스는 GetBufferHandle을 사용하여 버퍼를 식별하는 프로세스 독립 핸들을 가져올 수 있습니다. 그런 다음, 이 핸들은 동일한 가상 디바이스 세트가 열려 있는 다른 프로세스에 전달될 수 있습니다. 해당 프로세스는 ClientVirtualDeviceSet::MapBufferHandle을 사용하여 버퍼의 주소를 가져옵니다. 각 프로세스는 서로 다른 주소에서 버퍼를 매핑할 수 있으므로 이 주소는 파트너에 있는 주소와 다를 수 있습니다.

**구문** 

   ```
   int ClientVirtualDeviceSet::GetBufferHandle (
   uint8_t*     pBuffer,        // in: buffer address
   unsigned int*        pBufferHandle   // out: buffer handle
   );
   ```

| 매개 변수 | 인수 | 설명
| ----- | ----- | ------ |
| |**pBuffer** |Read 또는 Write 명령에서 가져온 버퍼의 주소입니다.
| |**BufferHandle** |버퍼의 고유 식별자가 반환됩니다.

| 반환 값 | 인수 | 설명
| ----- | ----- | ------ |
| |**NOERROR** |함수가 성공했습니다.
| |**VD_E_PROTOCOL** |가상 디바이스 세트가 현재 열려 있지 않습니다.
| |**VD_E_INVALID** |pBuffer가 유효한 주소가 아닙니다.

설명 GetBufferHandle 함수를 호출하는 프로세스는 데이터 전송이 완료될 때 ClientVirtualDevice::CompleteCommand를 호출해야 합니다.

## <a name="clientvirtualdevicesetmapbufferhandle"></a>ClientVirtualDeviceSet::MapBufferHandle

**용도** 이 함수는 일부 다른 프로세스에서 가져온 버퍼 핸들에서 유효한 버퍼 주소를 가져오는 데 사용됩니다. 

**구문** 

   ```
   int ClientVirtualDeviceSet::MapBufferHandle (
   i        nt  dwBuffer,   // in: buffer handle
   uint8_t**    ppBuffer        // out: buffer address
   );
   ```

| 매개 변수 | 인수 | 설명
| ----- | ----- | ------ |
| |**dwBuffer** |ClientVirtualDeviceSet::GetBufferHandle에서 반환되는 핸들입니다.
| |**ppBuffer** |현재 프로세스에서 유효한 버퍼의 주소입니다.

| 반환 값 | 인수 | 설명
| ----- | ----- | ------ |
| |**NOERROR** |함수가 성공했습니다.
| |**VD_E_PROTOCOL** |가상 디바이스 세트가 현재 열려 있지 않습니다.
| |**VD_E_INVALID** |ppBuffer가 잘못된 핸들입니다.

**설명** 핸들을 제대로 전달하기 위해 주의해야 합니다. 핸들은 단일 가상 디바이스 세트에 대해 로컬입니다. 핸들을 공유하는 파트너 프로세스는 버퍼 핸들이 원래 버퍼를 가져온 가상 디바이스 세트의 범위 내에서만 사용되는지 확인해야 합니다.


