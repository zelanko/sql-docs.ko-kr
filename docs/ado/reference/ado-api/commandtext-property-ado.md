---
title: "CommandText 속성 (ADO) | Microsoft Docs"
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
apitype: COM
f1_keywords:
- Command15::CommandText
helpviewer_keywords:
- CommandText property [ADO]
ms.assetid: 4dd7e82a-8da5-4a4e-b439-11a29286fa0e
caps.latest.revision: 12
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 60ee83c7d1f667feb0b1fcb4985dcd50edfda27b
ms.contentlocale: ko-kr
ms.lasthandoff: 09/09/2017

---
# <a name="commandtext-property-ado"></a>CommandText 속성 (ADO)
공급자에 대해 실행할 명령의 텍스트를 나타냅니다.  
  
## <a name="settings-and-return-values"></a>설정 및 반환 값  
 가져오거나는 **문자열** SQL 문, 테이블 이름, 상대 URL 또는 저장된 프로시저 호출 등의 공급자 명령을 포함 하는 값입니다. 기본값은 빈 문자열 ("").  
  
## <a name="remarks"></a>주의  
 사용 하 여는 **CommandText** 속성을 설정 하거나 반환할 나타내는 명령 텍스트는 [명령](../../../ado/reference/ado-api/command-object-ado.md) 개체입니다. 일반적으로 SQL 문을 이지만 다른 종류의 저장된 프로시저 호출과 같은 공급자가 인식 하는 명령 문은 수도 있습니다. SQL 문을 특정 언어나 공급자의 쿼리 프로세서에서 지 원하는 버전 이어야 합니다.  
  
 경우는 [Prepared](../../../ado/reference/ado-api/prepared-property-ado.md) 속성은 **명령** 개체로 설정 되어 **True** 및 **명령** 설정할 때 열려 있는 연결 개체가 바인딩된 **CommandText** ADO (즉, 컴파일된 형태를 공급자에 의해 저장 된 쿼리) 쿼리를 준비 속성을 호출 하는 경우는 [Execute](../../../ado/reference/ado-api/execute-method-ado-command.md) 또는 [열](../../../ado/reference/ado-api/open-method-ado-connection.md)메서드.  
  
 에 따라는 [CommandType](../../../ado/reference/ado-api/commandtype-property-ado.md) 속성 설정, ADO 변경 될 수는 **CommandText** 속성입니다. 읽을 수는 **CommandText** 속성 언제 든 지 실제 명령 텍스트를 실행 하는 동안 해당 ADO를 사용 합니다.  
  
 사용 하 여는 **CommandText** 속성을 설정 하거나 파일 또는 디렉터리와 같은 리소스를 지정 하는 상대 URL을 반환 합니다. 리소스를 명시적으로 또는 암시적으로 열려 있는 절대 URL을 통해 지정 된 위치에 상대적인 [연결](../../../ado/reference/ado-api/connection-object-ado.md) 개체입니다.  
  
> [!NOTE]
>  Url은 http 체계를 사용 하 여 자동으로 호출 됩니다는 [Microsoft OLE DB Provider for Internet Publishing](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-internet-publishing.md)합니다. 자세한 내용은 참조 [절대 경로 상대 Url](../../../ado/guide/data/absolute-and-relative-urls.md)합니다.  
  
## <a name="applies-to"></a>적용 대상  
 [명령 개체(ADO)](../../../ado/reference/ado-api/command-object-ado.md)  
  
## <a name="see-also"></a>관련 항목:  
 [ActiveConnection, CommandText, CommandTimeout, CommandType, 크기 및 방향 속성 예제 (VB)](../../../ado/reference/ado-api/activeconnection-commandtext-commandtimeout-commandtype-size-example-vb.md)   
 [ActiveConnection, CommandText, CommandTimeout, CommandType, 크기 및 방향 속성 예제 (VC + +)](../../../ado/reference/ado-api/activeconnection-commandtext-commandtimeout-commandtype-size-example-vc.md)   
 [Requery 메서드](../../../ado/reference/ado-api/requery-method.md)   
 [ActiveConnection, CommandText, CommandTimeout, CommandType, 크기 및 방향 속성 예제 (JScript)](../../../ado/reference/ado-api/activeconnection-commandtext-timeout-type-size-example-jscript.md)

