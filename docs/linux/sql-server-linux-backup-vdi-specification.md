---
title: VDI 백업 사양-Linux의 SQL Server | Microsoft Docs
description: SQL Server 가상 백업 장치 인터페이스 사양입니다.
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.date: 03/17/2017
ms.topic: conceptual
ms.prod: sql
ms.technology: linux
ms.assetid: 0250ba2b-8cdd-450e-9109-bf74f70e1247
ms.openlocfilehash: b3917f086361128ee0c3e0a73f44f2c7cc4049b6
ms.sourcegitcommit: 074d44994b6e84fe4552ad4843d2ce0882b92871
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/05/2019
ms.locfileid: "66713463"
---
# <a name="sql-server-on-linux-vdi-client-sdk-specification"></a>SQL Server Linux VDI 클라이언트 SDK 사양

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

이 문서에서는 Linux 가상 장치 인터페이스 (VDI) 클라이언트 SDK에서 SQL Server에서 제공 하는 인터페이스를 설명 합니다. 독립 소프트웨어 공급 업체 (Isv) 해당 제품에 SQL Server를 통합 하는 가상 백업 장치 응용 프로그램 프로그래밍 인터페이스 (API)를 사용할 수 있습니다. 일반적으로 Linux에서 VDI 비슷하게 Windows에서 VDI 다음 변경 내용으로:

- Windows 공유 메모리는 POSIX 공유 메모리를 됩니다.
- Windows 세마포 POSIX 세마포 수 있습니다.
- HRESULT 및 DWORD과 같은 Windows 종류를 정수로 변경 됩니다.
- COM 인터페이스 제거 되며 쌍을 사용 하 여 대체 C++ 클래스입니다.
- Linux의 SQL Server 인스턴스 이름에 대 한 참조가 제거 되었습니다 하므로 명명 된 인스턴스를 지원 하지 않습니다. 
- 공유 라이브러리 libsqlvdi.so /opt/mssql/lib/libsqlvdi.so 설치에서 구현 됩니다.

이 문서는 대 한 추 록 **vbackup.chm** Windows VDI 사양 세부 정보입니다. 다운로드 합니다 [Windows VDI 사양](https://www.microsoft.com/download/details.aspx?id=17282)합니다.

또한에서 샘플 VDI 백업 솔루션을 검토 합니다 [SQL Server 샘플 GitHub 리포지토리](https://github.com/Microsoft/sql-server-samples/tree/master/samples/features/sqlvdi-linux)합니다.

## <a name="user-permissions-setup"></a>사용자 권한 설정

Linux에서 POSIX 기본 형식 및 해당 기본 그룹을 만드는 사용자가 소유 합니다. SQL Server에서 만든 개체에 대 한 이러한 기본적으로 소유할 mssql 사용자 및 mssql 그룹입니다. SQL Server 및 VDI 클라이언트 간에 공유를 허용 하려면 다음 두 가지 방법 중 하나는 것이 좋습니다.

1. Mssql 사용자로 VDI 클라이언트를 실행 합니다.
   
   Mssql 사용자로 전환 하려면 다음 명령을 실행 합니다.
   
   ```bash
   sudo su mssql
   ```

2. Vdiuser의 그룹과 mssql 그룹 vdiuser mssql 사용자를 추가 합니다.
   
   다음 명령을 실행 합니다.

   ```bash
   sudo useradd vdiuser
   sudo usermod -a -G mssql vdiuser
   sudo usermod -a -G vdiuser mssql
   ```

   SQL Server 및 vdiuser에 대 한 새 그룹을 선택 하도록 서버를 다시 시작

## <a name="client-functions"></a>클라이언트 기능

이 장에서 각 클라이언트 함수를 설명 합니다. 설명에는 다음 정보가 포함 됩니다.

- 함수 용도
- 함수 구문
- 매개 변수 목록
- 반환 값
- Remarks

## <a name="clientvirtualdevicesetcreate"></a>ClientVirtualDeviceSet::Create

**목적은** 이 함수는 가상 장치 집합을 만듭니다.

**구문**
   ```
   int ClientVirtualDeviceSet::Create (
   char *   name,       // name for the set
   VDConfig   * cfg     // configuration for the set
   );
   ```

| 매개 변수 | 인수 | 설명
| ----- | ----- | ------ |
| | **name** | 가상 장치 집합을 식별합니다. CreateFileMapping()에서 사용 하는 이름에 대 한 규칙을 따라야 합니다. 백슬래시를 제외한 모든 문자 (\) 사용할 수 있습니다. 이 문자열입니다. 사용자의 제품 또는 회사 이름 및 데이터베이스 이름을 사용 하 여 문자열을 접두사로 하는 것이 좋습니다. |
| |**cfg** | 이 가상 장치 집합에 대 한 구성입니다. 자세한 내용은이 문서의 뒷부분에서 "구성"을 참조 하세요.

| 반환 값 | 인수 | 설명
| ----- | ----- | ------ |
| |**NOERROR** | 함수가 성공했습니다. |
| |**VD_E_NOTSUPPORTED** |구성에 있는 필드 중 하나 이상이 잘못 되었습니다. 그렇지 않은 경우 지원 되지 않는 합니다. |
| |**VD_E_PROTOCOL** | 가상 장치 집합이 이미 있습니다.

**주의** 당 백업 또는 복원 작업 만들기 메서드를 한 번만 호출 해야 합니다. Close 메서드를 호출한 후 클라이언트의 다른 가상 장치 집합을 만들 인터페이스를 다시 사용할 수 있습니다.

## <a name="clientvirtualdevicesetgetconfiguration"></a>ClientVirtualDeviceSet::GetConfiguration

**목적은** 이 함수는 가상 장치 집합을 구성 하려면 서버를 기다리는 데 사용 합니다.
**구문**
   ```
   int ClientVirtualDeviceSet::GetConfiguration (
   time_t       timeout,    // in milliseconds
   VDConfig *       cfg // selected configuration
   );
   ```

| 매개 변수 | 인수 | 설명
| ----- | ----- | ------ |
| | **timeout** | 제한 시간 (밀리초)입니다. 제한 시간을 방지 하기 위해 무한대 또는 음의 정수를 사용 합니다.
| | **cfg** | 성공적으로 실행 시 서버에서 선택한 구성을 포함 합니다. 자세한 내용은이 문서의 뒷부분에서 "구성"을 참조 하세요.

| 반환 값 | 인수 | 설명
| ----- | ----- | ------ |
| |**NOERROR** | 구성을 반환 되었습니다.
| |**VD_E_ABORT** |SignalAbort 호출 되었습니다.
| |**VD_E_TIMEOUT** |함수 제한 시간이 초과 되었습니다.

**주의** 진행 상태의이 함수를 차단 합니다. 성공적인 호출 후 가상 장치 집합에 연결 된 장치를 열 수 있습니다.


## <a name="clientvirtualdevicesetopendevice"></a>ClientVirtualDeviceSet::OpenDevice
**목적은** 이 함수는 장치 중 하나를 가상 장치 집합에서 열립니다.
**구문**
   ```
   int ClientVirtualDeviceSet::OpenDevice (
   char *           name,       // name for the set
   ClientVirtualDevice **       ppVirtualDevice // returns interface to device
   );
   ```

| 매개 변수 | 인수 | 설명
| ----- | ----- | ------ |
| | **name** |가상 장치 집합을 식별합니다.
| | **ppVirtualDevice** |함수가 성공 하면 가상 장치에 대 한 포인터를 반환 됩니다. 이 장치는 GetCommand CompleteCommand에 사용 됩니다.

| 반환 값 | 인수 | 설명
| ----- | ----- | ------ |
| |**NOERROR** |함수가 성공했습니다.
| |**VD_E_ABORT** | Abort는 요청 했습니다.
| |**VD_E_OPEN** |  모든 장치에 열려 있습니다.
| |**VD_E_PROTOCOL** |  집합 초기화 상태에 없거나이 특정 장치 이미 열려 있습니다.
| |**VD_E_INVALID** |장치 이름이 올바르지 않습니다. 이 집합을 구성 하는 특성 이름 중입니다.

**주의** VD_E_OPEN 문제 없이 반환 될 수 있습니다. 이 코드는 반환 될 때까지 클라이언트 루프를 사용 하 여 OpenDevice를 호출할 수 있습니다.
하나 이상의 장치가 구성 된 경우, 예를 들어 *n* 장치, 가상 장치 집합을 반환 합니다 *n* 고유한 장치 인터페이스입니다.

`GetConfiguration` 장치를 열 수 있습니다 때까지 대기 하는 함수를 사용할 수 있습니다.
이 함수가 성공 하지 못한 경우 null 값을 ppVirtualDevice 통해 반환 됩니다.
 
## <a name="clientvirtualdevicegetcommand"></a>ClientVirtualDevice::GetCommand

**용도** 이 함수는 다음을 가져오는 데 명령을 장치로 큐에 대기 합니다. 요청 하는 경우이 함수는 다음 명령에 대 한 대기 합니다.

**구문**
   ```
   int ClientVirtualDevice::GetCommand (
   time_t       timeout,    // time-out in milliseconds
   VDC_Command**    ppCmd   // returns the next command
   );
   ```

| 매개 변수 | 인수 | 설명
| ----- | ----- | ------ |
| |**timeout** |밀리초 단위로 대기 시간입니다. 무한 무기한 대기를 사용 합니다. 명령에 대해 폴링 하려면 0을 사용 합니다. 명령이 현재 사용 가능한 경우 VD_E_TIMEOUT 반환 됩니다. 시간 제한이 발생 하는 경우 클라이언트는 다음 작업을 결정 합니다.
| |**Timeout** |밀리초 단위로 대기 시간입니다. 무기한 대기를 무한 또는 음수 값을 사용 합니다. 명령에 대해 폴링 하려면 0을 사용 합니다. VD_E_TIMEOUT 제한 시간이 만료 되기 전에 없는 명령을 사용할 수 있는 경우 반환 됩니다. 시간 제한이 발생 하는 경우 클라이언트는 다음 작업을 결정 합니다.
| |**ppCmd** |명령을 성공적으로 반환 되 면 매개 변수는 명령이 실행의 주소를 반환 합니다. 반환 되는 메모리는 읽기 전용입니다. 명령이 완료 되 면이 포인터가 CompleteCommand 루틴에 전달 됩니다. 각 명령에 대 한 자세한 내용은이 문서의 뒷부분에서 "명령"을 참조 하십시오.
        
| 반환 값 | 인수 | 설명
| ----- | ----- | ------ |
| |**NOERROR** |명령을 가져온 합니다.
| |**VD_E_CLOSE** |장치는 서버에서 닫혔습니다.
| |**VD_E_TIMEOUT** |명령이 제공 되었으며 제한 시간이 만료 되었습니다.
| |**VD_E_ABORT** |클라이언트 또는 서버 하는 데는 SignalAbort 강제 종료 합니다.

**주의** 때 VD_E_CLOSE 반환 되 고, SQL Server가 장치를 닫았습니다. 정상적인 종료의 일부입니다. 모든 장치를 닫은 후에 클라이언트를 가상 장치 집합을 닫으려면 ClientVirtualDeviceSet::Close를 호출 합니다.
이 루틴을 명령에 대해 대기할 차단 해야 합니다. 스레드 경고 조건에서 그대로 사용 합니다.

## <a name="clientvirtualdevicecompletecommand"></a>ClientVirtualDevice::CompleteCommand

**목적은** 이 함수는 명령을 완료 하는 SQL Server에 알리기 위해 사용 합니다. 명령에 대 한 적절 한 완료 정보를 반환 합니다. 자세한 내용은이 문서의 뒷부분에서 "명령"을 참조 하세요.

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
| |**completionCode** |완료 상태를 나타내는 상태 코드입니다. 이 매개 변수는 모든 명령에 대 한 반환 되어야 합니다. 반환 되는 코드는 수행 중인 명령에 적합 해야 합니다. ERROR_SUCCESS 모든 경우에 성공적으로 실행된 명령을 나타내는 데 사용 됩니다. 가능한 코드의 전체 목록은 파일을 참조 하세요. vdierror.h 합니다. 각 명령에 대 한 일반적인 상태 코드 목록은이 문서의 뒷부분에서 "명령"에 나타납니다.
| |**bytesTransferred** |성공적으로 전송 된 바이트 수입니다. 데이터 전송 명령을 읽기 및 쓰기에 대해서만 반환 됩니다.
| |**position** |이것이 GetPosition 명령에 대 한 응답입니다.
        
| 반환 값 | 인수 | 설명
| ----- | ----- | ------ |
| |**NOERROR** |완료 올바르게 표시 합니다.
| |**VD_E_INVALID** |pCmd 활성 명령이 없습니다.
| |**VD_E_ABORT** |중단 된 신호를 받습니다.
| |**VD_E_PROTOCOL** |장치가 열려 있지 않습니다.

**주의** 없음

## <a name="clientvirtualdevicesetsignalabort"></a>ClientVirtualDeviceSet::SignalAbort

**목적은** 이 함수는 비정상적으로 종료 하 고 수행 되도록 신호를 사용 합니다.

**구문** 

   ```
   int ClientVirtualDeviceSet::SignalAbort ();
   ```

| 매개 변수 | 인수 | 설명
| ----- | ----- | ------ |
| |없음 | 해당 사항 없음
        
| 반환 값 | 인수 | 설명
| ----- | ----- | ------ |
| |**NOERROR**|중단 알림은 성공적으로 게시 되었습니다.

**주의** 언제 든 지, 클라이언트 백업 또는 복원 작업을 중단 하도록 선택할 수 있습니다. 이 루틴 모든 작업이 중단 되도록 신호를 보냅니다. 전체 가상 장치 집합의 상태를 비정상적으로 종료 상태로 설정 됩니다. 모든 장치에 없는 추가 명령이 반환 됩니다. 완료 되지 않은 모든 명령은 자동으로 완료 되 면 ERROR_OPERATION_ABORTED 완료 코드로 반환 합니다. 스레드가 처리 중인 클라이언트에 제공 하는 버퍼를 사용할 때 안전 하 게 종료 한 후 클라이언트에서 ClientVirtualDeviceSet::Close를 호출 해야 합니다. 자세한 내용은이 문서의 앞부분에서 "비정상 종료"를 참조 하세요.

## <a name="clientvirtualdevicesetclose"></a>ClientVirtualDeviceSet::Close

**목적은** 이 함수 ClientVirtualDeviceSet::Create에서 만든 가상 장치 집합을 닫습니다. 가상 장치 세트와 연결 된 모든 리소스의 릴리스에서 발생 합니다.

**구문** 

   ```
   int ClientVirtualDeviceSet::Close ();
   ```

| 매개 변수 | 인수 | 설명
| ----- | ----- | ------ |
| |없음 |해당 사항 없음
        
| 반환 값 | 인수 | 설명
| ----- | ----- | ------ |
| |**NOERROR** |가상 장치 집합을 성공적으로 닫은 경우 반환 됩니다.
| |**VD_E_PROTOCOL** |가상 장치 집합을 열고 없기 때문에 아무 작업도 수행 합니다.
| |**VD_E_OPEN** |장치 열려 있었습니다.

**주의** 닫기 호출 가상 장치 집합에서 사용 하는 모든 리소스가 해제 되어야 함을 클라이언트 선언입니다. 클라이언트는 Close를 호출 하기 전에 데이터 버퍼 및 가상 장치를 포함 하는 모든 작업을 종료 된 것을 확인 해야 합니다. 닫기 여 OpenDevice를 반환한 모든 가상 장치 인터페이스 무효화 됩니다.
클라이언트는 닫기 호출에서 반환 된 후 가상 장치 집합 인터페이스에 만들기 호출을 실행 하도록 허용 됩니다. 이러한 호출 후속 백업 또는 복원 작업에 대 한 설정으로 새 가상 장치를 만듭니다.
닫기는 하나 이상의 가상 장치를 계속 열려 있을 때 호출 되 면 VD_E_OPEN 반환 됩니다. 이 경우 SignalAbort 내부적으로 트리거될 가능한 경우 올바르게 종료 하 합니다. VDI 리소스가 해제 됩니다. 클라이언트는 ClientVirtualDeviceSet::Close를 호출 하기 전에 각 장치에서 VD_E_CLOSE 표시를 기다려야 합니다. 한다는 사실을 알고 있으면 클라이언트 가상 장치 집합 비정상적으로 종료 된 상태로 이미 다음을 기대 하지 않으면, GetCommand에서 VD_E_CLOSE 표시를 하 고 공유 버퍼에서 작업이 종료 되는 즉시 ClientVirtualDeviceSet::Close를 호출할 수 있습니다.
자세한 내용은이 문서의 앞부분에서 "비정상 종료"를 참조 하세요.

## <a name="clientvirtualdevicesetopeninsecondary"></a>ClientVirtualDeviceSet::OpenInSecondary

**목적은** 이 함수는 보조 클라이언트에서 설정 하는 가상 장치를 엽니다. 기본 클라이언트 해야는 이미 데 만들고 GetConfiguration 가상 장치 집합을 설정 합니다.

**구문** 
   
   ```
   int ClientVirtualDeviceSet::OpenInSecondary (
   char *   setName         // name of the set
   );
   ```

| 매개 변수 | 인수 | 설명
| ----- | ----- | ------ |
| |**setName** |이 집합을 식별 합니다. 이 이름은 대/소문자 구분 및 ClientVirtualDeviceSet::Create 호출 시 기본 클라이언트에서 사용한 이름과 일치 해야 합니다.

| 반환 값 | 인수 | 설명
| ----- | ----- | ------ |
| |**NOERROR** |함수가 성공했습니다.
| |**VD_E_PROTOCOL** |가상 장치 집합을 만들지 않은,이 클라이언트 또는 가상 장치에서 이미 열려 집합 보조 클라이언트로부터 열기 요청을 수락 하도록 준비 되지 않았습니다.
| |**VD_E_ABORT** |작업이 중단 됩니다.

**주의** 여러 프로세스 모델을 사용 하는 경우 기본 클라이언트는 보조 클라이언트의 정상 및 비정상적인 종료를 검색 합니다.

## <a name="clientvirtualdevicesetgetbufferhandle"></a>ClientVirtualDeviceSet::GetBufferHandle

**목적은** 일부 응용 프로그램 둘 이상의 프로세스 ClientVirtualDevice::GetCommand에서 반환 된 버퍼에서 작동 하도록 해야 할 수 있습니다. 이러한 경우 명령을 수신 하는 프로세스 버퍼를 식별 하는 프로세스 독립적 핸들을 얻기 위해 GetBufferHandle를 사용할 수 있습니다. 이 핸들도 동일한 가상 장치 설정 열려 있는 다른 프로세스에 게 전달 될 수 있습니다. 해당 프로세스는 사용 하 여 ClientVirtualDeviceSet::MapBufferHandle 버퍼의 주소를 가져옵니다. 주소 가능성이 됩니다와 다른 주소를 해당 파트너에 있으므로 각 프로세스에 서로 다른 주소에 대 한 버퍼 매핑 수 있습니다.

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
| |**VD_E_PROTOCOL** |가상 장치 집합을 현재 열려 있지 않습니다.
| |**VD_E_INVALID** |PBuffer를 유효한 주소가 아닙니다.

GetBufferHandle 함수를 호출 하는 프로세스는 데이터 전송이 완료 되 면 ClientVirtualDevice::CompleteCommand 호출에 대 한 설명입니다.

## <a name="clientvirtualdevicesetmapbufferhandle"></a>ClientVirtualDeviceSet::MapBufferHandle

**목적은** 이 함수에서 다른 프로세스에서 가져온 버퍼 핸들이 유효한 버퍼 주소를 가져오는 데 사용 됩니다. 

**구문** 

   ```
   int ClientVirtualDeviceSet::MapBufferHandle (
   i        nt  dwBuffer,   // in: buffer handle
   uint8_t**    ppBuffer        // out: buffer address
   );
   ```

| 매개 변수 | 인수 | 설명
| ----- | ----- | ------ |
| |**dwBuffer** |이것이 ClientVirtualDeviceSet::GetBufferHandle에서 반환한 핸들입니다.
| |**ppBuffer** |현재 프로세스에 적용 되는 버퍼의 주소입니다.

| 반환 값 | 인수 | 설명
| ----- | ----- | ------ |
| |**NOERROR** |함수가 성공했습니다.
| |**VD_E_PROTOCOL** |가상 장치 집합을 현재 열려 있지 않습니다.
| |**VD_E_INVALID** |ppBuffer 잘못 된 핸들입니다.

**주의** 핸들을 제대로 통신할 주의 해야 합니다. 핸들은 단일 가상 장치 집합에 로컬입니다. 핸들을 공유 하는 파트너 프로세스는 가상 장치는 버퍼를 가져온 원래 설정의 범위 내 에서만 처리 되는 해당 버퍼를 확인 해야 합니다.


