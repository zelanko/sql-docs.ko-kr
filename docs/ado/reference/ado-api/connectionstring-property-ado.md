---
title: ConnectionString 속성 (ADO) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.component: ado
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Connection15::ConnectionString
helpviewer_keywords:
- ConnectionString property [ADO]
ms.assetid: 3be75b75-4d36-4479-ab64-9a456869252a
caps.latest.revision: 18
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 7b34a524380439dba07d12aa74ef24a870ab8ccc
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="connectionstring-property-ado"></a>ConnectionString 속성 (ADO)
데이터 원본에 대 한 연결을 설정 하는 데 사용 되는 정보를 나타냅니다.  
  
## <a name="settings-and-return-values"></a>설정 및 반환 값  
 설정 하거나 반환는 **문자열** 값입니다.  
  
## <a name="remarks"></a>주의  
 사용 하 여는 **ConnectionString** 계열이 포함 된 자세한 연결 문자열을 전달 하 여 데이터 원본을 지정 하려면 속성 *인수* *= value* 문 구분 하 여 세미콜론입니다.  
  
 ADO 지원에 대 한 다섯 가지 인수는 **ConnectionString** 속성; ADO에서 처리 없이 공급자에 게 직접 다른 인수 전달 합니다. 인수 ADO에서 지 원하는 다음과 같습니다.  
  
|인수|Description|  
|--------------|-----------------|  
|*Provider=*|연결에 사용할 공급자의 이름을 지정 합니다.|  
|*파일 이름 =*|미리 설정 된 연결 정보를 포함 하는 공급자별 파일 (예를 들어 지속형된 데이터 원본 개체)의 이름을 지정 합니다.|  
|*원격 공급자 =*|클라이언트 연결을 열 때 사용할 공급자의 이름을 지정 합니다. (원격 데이터 서비스만 합니다.)|  
|*원격 서버 =*|클라이언트 연결을 열 때 사용할 서버 경로 이름을 지정 합니다. (원격 데이터 서비스만 합니다.)|  
|*URL=*|파일 또는 디렉터리와 같은 리소스를 식별 하는 절대 URL로 연결 문자열을 지정 합니다.|  
  
 설정한 후의 **ConnectionString** 속성 및 open의 [연결](../../../ado/reference/ado-api/connection-object-ado.md) 개체 공급자 내용을 변경할 수는 속성의 예를 들어 ADO 정의 된 인수 이름에 매핑하는 방법으로 해당 특정 공급자에 해당 합니다.  
  
 **ConnectionString** 속성에 사용 되는 값을 자동으로 상속 된 *ConnectionString* 의 인수는 [열려](../../../ado/reference/ado-api/open-method-ado-connection.md) 메서드, 현재 재정의할수있습니다 **ConnectionString** 하는 동안 속성에서 **열려** 메서드를 호출 합니다.  
  
 때문에 *파일 이름* 인수로 인해 연결 된 공급자를 로드 하는 ADO, 모두 전달할 수 없습니다는 *공급자* 및 *파일 이름* 인수입니다.  
  
 **ConnectionString** 속성은 읽기/쓰기 연결이 닫혀 있고 읽기 전용으로 열려 있으면입니다.  
  
 중 하나에 대 한 중복 된 **ConnectionString** 속성은 무시 됩니다. 인수 중 하나가의 마지막 인스턴스 사용 됩니다.  
  
> [!NOTE]
>  **원격 데이터 서비스 사용** 클라이언트 쪽에서 사용할 때 **연결** 개체는 **ConnectionString** 속성만 포함할 수는 *원격 공급자* 및 *원격 서버* 매개 변수입니다.  
  
 다음 표에서 각 Windows 운영 체제에 대 한 기본 ADO 공급자를 보여 줍니다.  
  
|기본 ADO 공급자|Windows 운영 체제|  
|--------------------------|------------------------------|  
|MSDASQL<br /><br /> (소스 코드의 가독성을 높이기 위해 명시적으로 지정 공급자 이름이 연결 문자열에 있습니다.)|Windows 2000 (32 비트)<br /><br /> Windows XP (32 비트)<br /><br /> Windows Server 2003 (32 비트)<br /><br /> Windows Vista (32 비트)<br /><br /> Windows Vista 서비스 팩 1 또는 이후 (32 비트 및 64 비트)<br /><br /> Windows Vista (32 비트 및 64 비트) 후 Windows 버전|  
|기본값은 없습니다.<br /><br /> ADO 응용 프로그램은 다음 운영 체제에서 실행 되며 공급자를 명시적으로 지정 하지 않습니다, ADO 반환 오류: "ADODB 합니다. 연결: 지정 된 기본 공급자가 및가 지정 되지 않았습니다 "|Windows 2000 (64 비트)<br /><br /> Windows XP (64 비트)<br /><br /> Windows Server 2003 (64 비트)<br /><br /> Windows Vista (64 비트)|  
  
## <a name="applies-to"></a>적용 대상  
 [연결 개체(ADO)](../../../ado/reference/ado-api/connection-object-ado.md)  
  
## <a name="see-also"></a>관련 항목:  
 [ConnectionString, ConnectionTimeout, 및 상태 속성 예제 (VB)](../../../ado/reference/ado-api/connectionstring-connectiontimeout-and-state-properties-example-vb.md)   
 [ConnectionString, ConnectionTimeout, 및 상태 속성 예제 (VC + +)](../../../ado/reference/ado-api/connectionstring-connectiontimeout-and-state-properties-example-vc.md)   
 [부록 A: 공급자](../../../ado/guide/appendixes/appendix-a-providers.md)
