---
description: ConnectionString 속성(ADO)
title: ConnectionString 속성 (ADO) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Connection15::ConnectionString
helpviewer_keywords:
- ConnectionString property [ADO]
ms.assetid: 3be75b75-4d36-4479-ab64-9a456869252a
author: rothja
ms.author: jroth
ms.openlocfilehash: 2add76a640e89bebe8a941afa5896bb2300750a9
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/27/2020
ms.locfileid: "88974774"
---
# <a name="connectionstring-property-ado"></a>ConnectionString 속성(ADO)
데이터 원본에 대 한 연결을 설정 하는 데 사용 되는 정보를 나타냅니다.  
  
## <a name="settings-and-return-values"></a>설정 및 반환 값  
 **문자열** 값을 설정 하거나 반환 합니다.  
  
## <a name="remarks"></a>설명  
 **ConnectionString** 속성을 사용 하 여 세미콜론으로 구분 된 일련의 *argument* *= value* 문을 포함 하는 자세한 연결 문자열을 전달 하 여 데이터 원본을 지정할 수 있습니다.  
  
 ADO는 **ConnectionString** 속성에 대해 5 개의 인수를 지원 합니다. 다른 모든 인수는 ADO에서 처리 하지 않고 공급자에 게 직접 전달 됩니다. ADO에서 지 원하는 인수는 다음과 같습니다.  
  
|인수|설명|  
|--------------|-----------------|  
|*공급자 =*|연결에 사용할 공급자의 이름을 지정 합니다.|  
|*파일 이름 =*|미리 설정 된 연결 정보를 포함 하는 공급자별 파일 (예: 지속형 데이터 원본 개체)의 이름을 지정 합니다.|  
|*원격 공급자 =*|클라이언트 쪽 연결을 열 때 사용할 공급자의 이름을 지정 합니다. (원격 데이터 서비스에만 해당)|  
|*원격 서버 =*|클라이언트 쪽 연결을 열 때 사용할 서버의 경로 이름을 지정 합니다. (원격 데이터 서비스에만 해당)|  
|*URL =*|파일 또는 디렉터리와 같은 리소스를 식별 하는 절대 URL로 연결 문자열을 지정 합니다.|  
  
 **ConnectionString** 속성을 설정 하 고 [연결](./connection-object-ado.md) 개체를 연 후에는 공급자가 속성의 콘텐츠를 변경할 수 있습니다. 예를 들어 ADO에서 정의한 인수 이름을 특정 공급자의 해당 항목에 매핑할 수 있습니다.  
  
 **Connectionstring** 속성은 [open](./open-method-ado-connection.md) 메서드의 *connectionstring* 인수에 사용 되는 값을 자동으로 상속 하므로 **open** 메서드 호출 중에 현재 **connectionstring** 속성을 재정의할 수 있습니다.  
  
 *파일 이름* 인수를 사용할 경우 ADO에서 연결 된 공급자를 로드 하므로 *공급자* 와 *파일 이름* 인수를 모두 전달할 수 없습니다.  
  
 **ConnectionString** 속성은 연결이 닫힌 경우 읽기/쓰기이 고, 열려 있으면 읽기 전용입니다.  
  
 **ConnectionString** 속성에서 인수의 중복은 무시 됩니다. 인수의 마지막 인스턴스가 사용 됩니다.  
  
> [!NOTE]
>  **원격 데이터 서비스 사용** 클라이언트 쪽 **연결** 개체에서 사용 하는 경우 **ConnectionString** 속성은 *원격 공급자* 및 *원격 서버* 매개 변수만 포함할 수 있습니다.  
  
 다음 표에서는 각 Windows 운영 체제에 대 한 기본 ADO 공급자를 보여 줍니다.  
  
|기본 ADO 공급자|Windows 운영 체제|  
|--------------------------|------------------------------|  
|MSDASQL<br /><br /> 소스 코드의 가독성을 높이기 위해 연결 문자열에서 공급자 이름을 명시적으로 지정 합니다.|Windows 2000 (32 비트)<br /><br /> Windows XP(32비트)<br /><br /> Windows 2003 서버 (32 비트)<br /><br /> Windows Vista(32비트)<br /><br /> Windows Vista 서비스 팩 1 이상 (32 비트 및 64 비트)<br /><br /> Windows Vista 이후 windows 버전 (32 비트 및 64 비트)|  
|기본값은 없습니다.<br /><br /> ADO 응용 프로그램이 다음 운영 체제에서 실행 되 고 공급자를 명시적으로 지정 하지 않은 경우 ADO에서 다음 오류를 반환 합니다. "ADODB. 연결: 공급자가 지정 되지 않았고 지정 된 기본 공급자가 없습니다. "|Windows 2000 (64 비트)<br /><br /> Windows XP(64비트)<br /><br /> Windows 2003 서버 (64 비트)<br /><br /> Windows Vista(64비트)|  
  
## <a name="applies-to"></a>적용 대상  
 [연결 개체(ADO)](./connection-object-ado.md)  
  
## <a name="see-also"></a>참고 항목  
 [ConnectionString, ConnectionTimeout 및 State 속성 예제 (VB)](./connectionstring-connectiontimeout-and-state-properties-example-vb.md)   
 [ConnectionString, ConnectionTimeout 및 State 속성 예제 (VC + +)](./connectionstring-connectiontimeout-and-state-properties-example-vc.md)   
 [부록 A: 공급자](../../guide/appendixes/appendix-a-providers.md)