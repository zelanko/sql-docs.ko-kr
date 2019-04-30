---
title: ConnectionString 속성 (ADO) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 01a930bc571e84c6ecfd38ce8415493c90ebd377
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "63140361"
---
# <a name="connectionstring-property-ado"></a>ConnectionString 속성(ADO)
데이터 원본에 연결 하는 데 사용 하는 정보를 나타냅니다.  
  
## <a name="settings-and-return-values"></a>설정 및 반환 값  
 설정 하거나 반환 된 **문자열** 값입니다.  
  
## <a name="remarks"></a>Remarks  
 사용 합니다 **ConnectionString** 계열이 포함 된 자세한 연결 문자열을 전달 하 여 데이터 원본을 지정 하려면 속성 *인수* *= value* 로 문 구분 세미콜론으로 구분 합니다.  
  
 ADO에 대 한 다섯 개의 인수를 지원 합니다 **ConnectionString** 속성; ADO에서 처리 하지 않고 공급자에 직접 다른 인수 전달 합니다. 인수 ADO 지원은 다음과 같습니다.  
  
|인수|Description|  
|--------------|-----------------|  
|*Provider=*|연결에 사용할 공급자의 이름을 지정 합니다.|  
|*파일 이름 =*|미리 설정 된 연결 정보를 포함 하는 공급자별 파일 (예를 들어 지속형된 데이터 원본 개체)의 이름을 지정 합니다.|  
|*원격 공급자 =*|클라이언트 쪽 연결을 열 때 사용할 공급자의 이름을 지정 합니다. (원격 데이터 서비스만 해당입니다.)|  
|*Remote Server=*|클라이언트 쪽 연결을 열 때 사용할 서버를의 경로 이름을 지정 합니다. (원격 데이터 서비스만 해당입니다.)|  
|*URL=*|파일 또는 디렉터리와 같은 리소스를 식별 하는 절대 URL로 연결 문자열을 지정 합니다.|  
  
 설정한 후는 **ConnectionString** 속성 및 open 합니다 [연결](../../../ado/reference/ado-api/connection-object-ado.md) 개체 공급자 내용을 변경할 수 속성의 예를 들어 ADO 정의한 인수 이름에 매핑하여 해당 특정 공급자에 해당 합니다.  
  
 **ConnectionString** 속성에 사용 된 값을 자동으로 상속 합니다 *ConnectionString* 인수의 합니다 [열기](../../../ado/reference/ado-api/open-method-ado-connection.md) 메서드, 현재 재정의할수있습니다 **ConnectionString** 중에 속성을 **열기** 메서드를 호출 합니다.  
  
 때문에 *파일 이름* 인수를 사용 하면 연결된 공급자를 로드할 수는 ADO, 모두 전달할 수 없습니다는 *공급자* 하 고 *파일 이름* 인수입니다.  
  
 합니다 **ConnectionString** 를 열었을 때 닫혀 있고 읽기 전용으로 연결 되 면 속성은 읽기/쓰기입니다.  
  
 인수는 중복 된 **ConnectionString** 속성은 무시 됩니다. 마지막 인스턴스의 인수가 사용 됩니다.  
  
> [!NOTE]
>  **원격 데이터 서비스 사용** 클라이언트 쪽에서 사용할 때 **연결** 개체를 **ConnectionString** 속성만 포함할 수는 *원격 공급자* 및 *원격 서버* 매개 변수입니다.  
  
 다음 표에서 각 Windows 운영 체제에 대 한 기본 ADO 공급자를 나열합니다.  
  
|기본 ADO 공급자|Windows 운영 체제|  
|--------------------------|------------------------------|  
|MSDASQL<br /><br /> (소스 코드의 가독성을 높이기 이름을 명시적으로 지정 된 공급자 연결 문자열에.)|Windows 2000 (32 비트)<br /><br /> Windows XP (32 비트)<br /><br /> Windows Server 2003 (32 비트)<br /><br /> Windows Vista (32 비트)<br /><br /> Windows Vista 서비스 팩 1 또는 이후 (32 비트 및 64 비트)<br /><br /> Windows Vista (32 비트 및 64 비트) 이후 Windows 버전|  
|기본값은 없습니다.<br /><br /> ADO 응용 프로그램은 다음 운영 체제에서 실행 되며 공급자를 명시적으로 지정 하지 않습니다, ADO 다음 오류를 반환 합니다. "ADODB 합니다. 연결: 공급자를 지정 하지 않으면 이며 지정 된 기본 공급자가 없습니다 "|Windows 2000 (64 비트)<br /><br /> Windows XP (64 비트)<br /><br /> Windows Server 2003 (64 비트)<br /><br /> Windows Vista (64 비트)|  
  
## <a name="applies-to"></a>적용 대상  
 [연결 개체(ADO)](../../../ado/reference/ado-api/connection-object-ado.md)  
  
## <a name="see-also"></a>관련 항목  
 [ConnectionString, ConnectionTimeout, 및 State 속성 예제 (VB)](../../../ado/reference/ado-api/connectionstring-connectiontimeout-and-state-properties-example-vb.md)   
 [ConnectionString, ConnectionTimeout, 및 State 속성 예제 (VC + +)](../../../ado/reference/ado-api/connectionstring-connectiontimeout-and-state-properties-example-vc.md)   
 [부록 a: 공급자](../../../ado/guide/appendixes/appendix-a-providers.md)
