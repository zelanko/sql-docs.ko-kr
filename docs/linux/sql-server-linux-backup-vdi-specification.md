---
title: "VDI 백업 사양-Linux에서 SQL Server | Microsoft Docs"
description: "SQL Server 가상 백업 장치 인터페이스 사양입니다."
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.date: 03/17/2017
ms.topic: article
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: 
ms.suite: sql
ms.custom: sql-linux
ms.technology: database-engine
ms.assetid: 0250ba2b-8cdd-450e-9109-bf74f70e1247
ms.workload: Inactive
ms.openlocfilehash: 9760b93a1e224c35617b4161d8996ff0ed3dff67
ms.sourcegitcommit: f02598eb8665a9c2dc01991c36f27943701fdd2d
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/13/2018
---
# <a name="sql-server-on-linux-vdi-client-sdk-specification"></a>Linux VDI 클라이언트 SDK 사양에서 SQL Server

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

이 문서에서는 Linux 가상 장치 인터페이스 (VDI) 클라이언트 SDK에는 SQL Server에서 제공 하는 인터페이스에 설명 합니다. 독립 소프트웨어 공급 업체 (Isv) SQL Server의 제품에 통합 하는 가상 백업 장치 API 응용 프로그래밍 인터페이스 ()를 사용할 수 있습니다. 일반적으로 Linux에서 VDI 유사 하 게 작동 VDI Windows에서 다음과 같이 변경 된:

- Windows 공유 메모리 POSIX 공유 메모리 됩니다.
- Windows 세마포 POSIX 세마포 수 있습니다.
- HRESULT 및 DWORD과 같은 Windows 종류는 정수 형식으로 변경 됩니다.
- COM 인터페이스는 제거 되 고 c + + 클래스의 쌍으로 바뀝니다.
- Linux에서 SQL Server 인스턴스 이름에 대 한 참조를 제거 명명 된 인스턴스를 지원 하지 않습니다. 
- 공유 라이브러리 libsqlvdi.so /opt/mssql/lib/libsqlvdi.so에 설치에서 구현 됩니다.

이 문서는 파일의 부록 **vbackup.chm** Windows VDI 사양에 자세히 설명 하는 합니다. 다운로드는 [Windows VDI 사양](http://www.microsoft.com/download/details.aspx?id=17282)합니다.

또한에 샘플 VDI 백업 솔루션을 검토는 [SQL Server 샘플 GitHub 리포지토리](http://github.com/Microsoft/sql-server-samples/tree/master/samples/features/sqlvdi-linux)합니다.

## <a name="user-permissions-setup"></a>사용자 권한 설정

Linux에서 POSIX 기본 형식 및 해당 기본 그룹을 만드는 사용자가 소유 합니다. SQL Server에서 만든 개체에 대 한 이러한 기본적으로 소유할 mssql 사용자 및 mssql 그룹입니다. SQL Server와 VDI 클라이언트 간 공유를 허용 하려면 다음 두 가지 방법 중 하나는 것이 좋습니다.

1. Mssql 사용자로 VDI 클라이언트를 실행 합니다.
   
   Mssql 사용자로 전환 하려면 다음 명령을 실행 합니다.
   
   ```bash
   sudo su mssql
   ```

2. Mssql 사용자 vdiuser의 그룹과 vdiuser mssql 그룹에 추가 합니다.
   
   다음 명령을 실행 합니다.

   ```bash
   sudo useradd vdiuser
   sudo usermod -a -G mssql vdiuser
   sudo usermod -a -G vdiuser mssql
   ```

   SQL Server 및 vdiuser에 대 한 새 그룹을 선택 하도록 서버를 다시 시작

## <a name="client-functions"></a>클라이언트 기능

이 장에서 설명의 각 클라이언트 함수를 포함합니다. 설명에는 다음 정보가 포함 됩니다.

- 함수 용도
- 함수 구문
- 매개 변수 목록
- 반환 값
- 주의

## <a name="clientvirtualdevicesetcreate"></a>ClientVirtualDeviceSet::Create

**용도** 이 함수는 가상 장치 집합을 만듭니다.

**구문**
   ```
   int ClientVirtualDeviceSet::Create (
   char *   name,       // name for the set
   VDConfig   * cfg     // configuration for the set
   );
   ```

| 매개 변수 | 인수 | 설명
| ----- | ----- | ------ |
| | **name** | 가상 장치 집합을 식별 합니다. CreateFileMapping()에서 사용 되는 이름에 대 한 규칙을 따라야 합니다. 백슬래시를 제외한 모든 문자 (\) 사용할 수 있습니다. 문자 문자열입니다. 사용자의 제품 또는 회사 이름 및 데이터베이스 이름을 사용 하 여 문자열을 접두사로 사용 하는 것이 좋습니다. |
| |**cfg** | 이것이 가상 장치 집합에 대 한 구성입니다. 자세한 내용은이 문서의 뒷부분에 나오는 "구성"을 참조 합니다.

| 반환 값 | 인수 | 설명
| ----- | ----- | ------ |
| |**NOERROR** | 함수가 성공했습니다. |
| |**VD_E_NOTSUPPORTED** |구성에서 필드의 하나 이상이 잘못 되었습니다. 또는 그렇지 않은 경우 지원 되지 않습니다. |
| |**VD_E_PROTOCOL** | 가상 장치 집합이 이미 있습니다.

**주의** The Create 메서드는 백업 또는 복원 작업 당 한 번만 호출 해야 합니다. Close 메서드를 호출한 후 클라이언트를 다른 가상 장치 집합을 만들려면 인터페이스 다시 사용할 수 있습니다.

## <a name="clientvirtualdevicesetgetconfiguration"></a>ClientVirtualDeviceSet::GetConfiguration

**용도** 이 함수는 가상 장치 집합을 구성 하는 서버를 기다리는 데 사용 합니다.
**구문**
   ```
   int ClientVirtualDeviceSet::GetConfiguration (
   time_t       timeout,    // in milliseconds
   VDConfig *       cfg // selected configuration
   );
   ```

| 매개 변수 | 인수 | 설명
| ----- | ----- | ------ |
| | **timeout** | 제한 시간 (밀리초)입니다. 제한 시간을 방지 하기 위해 무한 또는 모든 음의 정수를 사용 합니다.
| | **cfg** | 실행이 완료 되는 서버에서 선택한 구성에 포함 되어이 있습니다. 자세한 내용은이 문서의 뒷부분에 나오는 "구성"을 참조 합니다.

| 반환 값 | 인수 | 설명
| ----- | ----- | ------ |
| |**NOERROR** | 구성을 반환 되었습니다.
| |**VD_E_ABORT** |SignalAbort 호출 되었습니다.
| |**VD_E_TIMEOUT** |함수 제한 시간이 초과 되었습니다.

**주의** 경고 상태에이 함수를 차단 합니다. 성공적으로 호출 후 가상 장치 집합의 장치를 열 수 있습니다.


## <a name="clientvirtualdevicesetopendevice"></a>ClientVirtualDeviceSet::OpenDevice
**용도** 이 함수는 가상 장치 집합의 장치 중 하나를 엽니다.
**구문**
   ```
   int ClientVirtualDeviceSet::OpenDevice (
   char *           name,       // name for the set
   ClientVirtualDevice **       ppVirtualDevice // returns interface to device
   );
   ```

| 매개 변수 | 인수 | 설명
| ----- | ----- | ------ |
| | **name** |가상 장치 집합을 식별 합니다.
| | **ppVirtualDevice** |함수가 성공 하면 가상 장치에 대 한 포인터를 반환 됩니다. 이 장치는 GetCommand 및 CompleteCommand에 사용 됩니다.

| 반환 값 | 인수 | 설명
| ----- | ----- | ------ |
| |**NOERROR** |함수가 성공했습니다.
| |**VD_E_ABORT** | 중단을 요청 합니다.
| |**VD_E_OPEN** |  모든 장치에 열려 있습니다.
| |**VD_E_PROTOCOL** |  집합 초기화 상태에 없거나이 특정 장치 이미 열려 있습니다.
| |**VD_E_INVALID** |장치 이름이 잘못 되었습니다. 이기는 집합을 구성 하는 특성 이름 중 하나입니다.

**주의** VD_E_OPEN 문제 없이 반환 될 수 있습니다. 클라이언트는이 코드에 반환 될 때까지 OpenDevice 루프를 사용 하 여 호출할 수 있습니다.
하나 이상의 장치가 구성 된 경우, 예를 들어  *n*  장치, 가상 장치 집합이 반환 됩니다  *n*  고유 장치 인터페이스입니다.

`GetConfiguration` 장치를 열 수까지 기다렸다가 함수를 사용할 수 있습니다.
이 함수 이어지지 않는 경우는 ppVirtualDevice 통해 null 값이 반환 됩니다.
 
## <a name="clientvirtualdevicegetcommand"></a>ClientVirtualDevice::GetCommand

**용도** 이 함수는 다음을 가져오는 데 명령은 장치에 큐에 대기 합니다. 요청 하는 경우이 함수는 다음 명령에 대 한 대기 합니다.

**구문**
   ```
   int ClientVirtualDevice::GetCommand (
   time_t       timeout,    // time-out in milliseconds
   VDC_Command**    ppCmd   // returns the next command
   );
   ```

| 매개 변수 | 인수 | 설명
| ----- | ----- | ------ |
| |**timeout** |밀리초에서 대기 하는 시간입니다. INFINTE를 사용 하 여 무기한 대기를 나타냅니다. 명령에 대 한 폴링 0을 사용 합니다. 명령이 현재 사용 가능한 경우 VD_E_TIMEOUT 반환 됩니다. 제한 시간이 발생 하는 경우 클라이언트는 다음 동작을 결정 합니다.
| |**Timeout** |밀리초에서 대기 하는 시간입니다. INFINTE 또는 음수 값을 사용 하 여 무기한 대기를 나타냅니다. 명령에 대 한 폴링 0을 사용 합니다. VD_E_TIMEOUT 제한 시간이 만료 되기 전에 명령이 없습니다. 사용할 수 있는 경우 반환 됩니다. 제한 시간이 발생 하는 경우 클라이언트는 다음 동작을 결정 합니다.
| |**ppCmd** |명령을 성공적으로 반환 되 면 매개 변수는 명령이 실행의 주소를 반환 합니다. 반환 되는 메모리는 읽기 전용입니다. 명령이 완료 되 면이 포인터가 CompleteCommand 루틴에 전달 됩니다. 각 명령에 대 한 내용은이 문서의 뒷부분에 나오는 "Commands"를 참조 하십시오.
        
| 반환 값 | 인수 | 설명
| ----- | ----- | ------ |
| |**NOERROR** |명령을 인출 되었습니다.
| |**VD_E_CLOSE** |장치가 서버에 의해 종료 되었습니다.
| |**VD_E_TIMEOUT** |명령이 없습니다. 제공 되었으며 제한 시간이 만료 되었습니다.
| |**VD_E_ABORT** |클라이언트나 서버 어느 한쪽을 종료할는 SignalAbort 사용 했습니다.

**주의** 했습니다 때 반환 되 고, SQL Server 장치를 닫았습니다. 이 정상적인 종료의 일부입니다. 모든 장치를 닫은 후 클라이언트를 가상 장치 집합을 닫으려면 ClientVirtualDeviceSet::Close를 호출 합니다.
이 루틴에 명령에 대해 기다려야 차단 해야 합니다. 스레드는 경고 조건에 남아 있습니다.

## <a name="clientvirtualdevicecompletecommand"></a>ClientVirtualDevice::CompleteCommand

**용도** 이 함수는 명령이 완료 된 SQL Server를 알리는 데 사용 됩니다. 명령에 대 한 적절 한 완료 정보를 반환 합니다. 자세한 내용은이 문서의 뒷부분에 나오는 "Commands"를 참조 하십시오.

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
| |**pCmd** |ClientVirtualDevice::GetCommand에서 이전에 반환 되는 명령의 주소입니다.
| |**completionCode** |완료 상태를 나타내는 상태 코드입니다. 이 매개 변수는 모든 명령에 대 한 반환 되어야 합니다. 반환 되는 코드는 수행 중인 명령에 적합 해야 합니다. ERROR_SUCCESS 모든 경우에에서 성공적으로 실행 된 명령을 나타내는 데 사용 됩니다. 참조 파일을 가능한 코드의 전체 목록은 vdierror.h 합니다. 각 명령에 대 한 일반적인 상태 코드 목록은이 문서의 뒷부분에 나오는 "명령"에 나타납니다.
| |**bytesTransferred** |성공적으로 전송 된 바이트 수입니다. 데이터 전송 명령을 읽기 및 쓰기에 대해서만 반환 됩니다.
| |**position** |이것이 GetPosition 명령에 대 한 응답입니다.
        
| 반환 값 | 인수 | 설명
| ----- | ----- | ------ |
| |**NOERROR** |완료 올바르게 표시 합니다.
| |**VD_E_INVALID** |pCmd 활성 명령이 없습니다.
| |**VD_E_ABORT** |중단 신호를 받은 합니다.
| |**VD_E_PROTOCOL** |장치가 열려 있지 않습니다.

**주의** 없음

## <a name="clientvirtualdevicesetsignalabort"></a>ClientVirtualDeviceSet::SignalAbort

**용도** 경우 비정상적인 종료 하 고 수행 되도록 신호를 보내이 함수는 사용 합니다.

**구문** 

   ```
   int ClientVirtualDeviceSet::SignalAbort ();
   ```

| 매개 변수 | 인수 | 설명
| ----- | ----- | ------ |
| |InclusionThresholdSetting | 해당 사항 없음
        
| 반환 값 | 인수 | 설명
| ----- | ----- | ------ |
| |**NOERROR**|중단 알림이 성공적으로 게시 되었습니다.

**주의** 언제 든 지, 클라이언트 백업 또는 복원 작업을 중단 하도록 선택할 수 있습니다. 이 루틴 모든 작업이 중단 되도록 신호를 보냅니다. 전체 가상 장치 집합의 상태는 비정상적으로 종료 된 상태로 설정 됩니다. 모든 장치에 더 추가 명령이 반환 됩니다. 완료 되지 않은 모든 명령은 자동으로 완료 되 면 ERROR_OPERATION_ABORTED 완료 코드로 반환 합니다. 클라이언트는 클라이언트에 제공 하는 버퍼의 처리 중인 사용 되는 모든 모음이 안전 하 게 끝난 다음 ClientVirtualDeviceSet::Close를 호출 해야 합니다. 자세한 내용은이 문서의 앞부분에서 "비정상적으로 종료"를 참조 하십시오.

## <a name="clientvirtualdevicesetclose"></a>ClientVirtualDeviceSet::Close

**용도** 이 함수 ClientVirtualDeviceSet::Create에서 만든 가상 장치 집합을 닫습니다. 가상 장치 세트와 연결 된 모든 리소스의 릴리스에서 발생 합니다.

**구문** 

   ```
   int ClientVirtualDeviceSet::Close ();
   ```

| 매개 변수 | 인수 | 설명
| ----- | ----- | ------ |
| |InclusionThresholdSetting |해당 사항 없음
        
| 반환 값 | 인수 | 설명
| ----- | ----- | ------ |
| |**NOERROR** |가상 장치 집합이 성공적으로 닫혔을 때 반환 됩니다.
| |**VD_E_PROTOCOL** |가상 장치 집합 열기 없기 때문에 아무 작업도 수행 합니다.
| |**VD_E_OPEN** |장치 된 아직 열려 있습니다.

**주의** Close의 호출에는 가상 장치 집합에서 사용 하는 모든 리소스를 해제 해야 클라이언트 선언입니다. 클라이언트는 데이터 버퍼 및 가상 장치를 포함 하는 모든 작업은 Close를 호출 하기 전에 종료 되도록 확인 해야 합니다. 닫기를 OpenDevice에서 반환 된 모든 가상 장치 인터페이스를 무효화 합니다.
클라이언트 닫기 호출에서 반환 된 후 가상 장치 집합 인터페이스에 만들기 호출을 실행할 수 있습니다. 이러한 호출을 후속 백업 또는 복원 작업에 대해 설정 하는 새 가상 장치를 만듭니다.
Close는 하나 이상의 가상 장치 계속 열려 있는 경우에 호출 되 면 VD_E_OPEN 반환 됩니다. 이 경우 SignalAbort 내부적으로 트리거된 가능한 경우 올바르게 종료 하 합니다. VDI 리소스가 해제 됩니다. ClientVirtualDeviceSet::Close 호출 하기 전에 각 장치에서 했습니다 표시에 대 한 대기 해야 합니다. 한다는 사실을 알고 있으면 클라이언트는 가상 장치 집합 이미 비정상적으로 종료 된 상태에 있는 경우, GetCommand에서 했습니다 표시 기대 하지 하 고 공유 버퍼에서 작업이 종료 되는 즉시 ClientVirtualDeviceSet::Close을 호출할 수도 있습니다.
자세한 내용은이 문서의 앞부분에서 "비정상적으로 종료"를 참조 하십시오.

## <a name="clientvirtualdevicesetopeninsecondary"></a>ClientVirtualDeviceSet::OpenInSecondary

**용도** 이 기능은 보조 클라이언트에서에서 설정할 가상 장치를 엽니다. 기본 클라이언트 해야 이미 사용 했습니다 만들기 및 GetConfiguration 가상 장치 집합을 설정 하려면.

**구문** 
   
   ```
   int ClientVirtualDeviceSet::OpenInSecondary (
   char *   setName         // name of the set
   );
   ```

| 매개 변수 | 인수 | 설명
| ----- | ----- | ------ |
| |**setName** |집합을 식별 합니다. 이 이름은 대 소문자를 구분 하며 ClientVirtualDeviceSet::Create 호출 때 기본 클라이언트에서 사용 하는 이름과 일치 해야 합니다.

| 반환 값 | 인수 | 설명
| ----- | ----- | ------ |
| |**NOERROR** |함수가 성공했습니다.
| |**VD_E_PROTOCOL** |가상 장치 집합 생성 되지 않은,이 클라이언트 또는 가상 장치에서 이미 열려 집합이 보조 클라이언트로부터 열기 요청을 수락할 준비가 되었습니다.
| |**VD_E_ABORT** |작업이 중단 되 고 됩니다.

**주의** 다중 프로세스 모델을 사용할 때 기본 클라이언트는 보조 클라이언트의 정상 및 비정상 종료를 담당 합니다.

## <a name="clientvirtualdevicesetgetbufferhandle"></a>ClientVirtualDeviceSet::GetBufferHandle

**용도** 일부 응용 프로그램에는 둘 이상의 프로세스가 ClientVirtualDevice::GetCommand에서 반환 된 버퍼에서 작동 하도록 해야 할 수 있습니다. 이러한 경우 명령을 받는 프로세스는 버퍼를 식별 하는 프로세스 독립 핸들을 얻기 위해 GetBufferHandle에서 사용할 수 있습니다. 이 핸들도 동일한 가상 장치 설정 열려 있는 모든 다른 프로세스에 게 알려 줄 수 수 있습니다. 그런 다음 해당 프로세스는 버퍼의 주소를 가져올 ClientVirtualDeviceSet::MapBufferHandle를 사용 합니다. 주소는 각 프로세스에 버퍼 다른 주소에 매핑 수 때문에 해당 파트너에 보다 다른 주소를 수 있습니다.

**구문** 

   ```
   int ClientVirtualDeviceSet::GetBufferHandle (
   uint8_t*     pBuffer,        // in: buffer address
   unsigned int*        pBufferHandle   // out: buffer handle
   );
   ```

| 매개 변수 | 인수 | 설명
| ----- | ----- | ------ |
| |**pBuffer** |읽기 또는 쓰기 명령에서 가져온 버퍼의 주소입니다.
| |**BufferHandle** |버퍼에 대 한 고유 식별자가 반환 됩니다.

| 반환 값 | 인수 | 설명
| ----- | ----- | ------ |
| |**NOERROR** |함수가 성공했습니다.
| |**VD_E_PROTOCOL** |가상 장치 집합이 현재 열려 있지 않습니다.
| |**VD_E_INVALID** |PBuffer의 유효한 주소가 아닙니다.
주의 GetBufferHandle 함수를 호출 하는 프로세스를 ClientVirtualDevice::CompleteCommand 데이터 전송이 완료 될 때 호출 됩니다.

## <a name="clientvirtualdevicesetmapbufferhandle"></a>ClientVirtualDeviceSet::MapBufferHandle

**용도** 이 함수는 다른 프로세스에서 얻은 버퍼 핸들에서 유효한 버퍼 주소를 사용 합니다. 

**구문** 

   ```
   int ClientVirtualDeviceSet::MapBufferHandle (
   i        nt  dwBuffer,   // in: buffer handle
   uint8_t**    ppBuffer        // out: buffer address
   );
   ```

| 매개 변수 | 인수 | 설명
| ----- | ----- | ------ |
| |**dwBuffer** |ClientVirtualDeviceSet::GetBufferHandle에서 반환 된 핸들입니다.
| |**ppBuffer** |현재 프로세스에 사용할 버퍼의 주소입니다.

| 반환 값 | 인수 | 설명
| ----- | ----- | ------ |
| |**NOERROR** |함수가 성공했습니다.
| |**VD_E_PROTOCOL** |가상 장치 집합이 현재 열려 있지 않습니다.
| |**VD_E_INVALID** |ppBuffer 잘못 된 핸들입니다.

**주의** 핸들을 제대로 통신 하도록 주의 해야 합니다. 핸들은 단일 가상 장치 집합에 로컬입니다. 핸들을 공유 하는 파트너 프로세스 핸들을 사용 하는 버퍼를 원래 얻어에서 설정할 가상 장치의 범위 내 에서만 해당 버퍼를 확인 해야 합니다.


