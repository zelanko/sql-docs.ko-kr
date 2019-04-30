---
title: CommandText 속성 (ADO) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Command15::CommandText
helpviewer_keywords:
- CommandText property [ADO]
ms.assetid: 4dd7e82a-8da5-4a4e-b439-11a29286fa0e
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: e9593b45e8b336fe777b8e240061e82c23543c1d
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "63316174"
---
# <a name="commandtext-property-ado"></a>CommandText 속성(ADO)
공급자에 대해 실행할 명령의 텍스트를 나타냅니다.  
  
## <a name="settings-and-return-values"></a>설정 및 반환 값  
 가져오거나를 **문자열** SQL 문, 테이블 이름, 상대 URL 또는 저장된 프로시저와 같은 공급자 명령을 포함 하는 값입니다. 기본값은 빈 문자열 ("").  
  
## <a name="remarks"></a>Remarks  
 사용 합니다 **CommandText** 나타내는 명령의 텍스트를 반환 하는 속성을 [명령](../../../ado/reference/ado-api/command-object-ado.md) 개체입니다. 일반적으로이 SQL 문을 있지만 다른 유형의 저장된 프로시저 호출과 같은 공급자가 인식 하는 명령 문 수도 있습니다. 특정 언어 또는 공급자의 쿼리 프로세서에서 지 원하는 버전의 SQL 문 이어야 합니다.  
  
 경우는 [Prepared](../../../ado/reference/ado-api/prepared-property-ado.md) 의 속성을 **명령** 개체로 설정 됩니다 **True** 및 **명령** 설정 하는 경우 개체에 대해 열린 연결에 바인딩된 **CommandText** 속성인 ADO 준비 쿼리 (즉, 공급자가 저장 되는 쿼리의 컴파일된 폼) 호출 하는 경우를 [Execute](../../../ado/reference/ado-api/execute-method-ado-command.md) 또는 [엽니다](../../../ado/reference/ado-api/open-method-ado-connection.md)메서드.  
  
 에 따라 합니다 [CommandType](../../../ado/reference/ado-api/commandtype-property-ado.md) 속성 설정을 ADO 변경 될 수는 **CommandText** 속성입니다. 읽을 수는 **CommandText** 언제 든 지 실제 명령 텍스트를 보려면 속성 실행 하는 동안 해당 ADO를 사용 합니다.  
  
 사용 된 **CommandText** 속성을 설정 하거나 파일 또는 디렉터리와 같은 리소스를 지정 하는 상대 URL을 반환 합니다. 리소스 또는 암시적으로 개방적이 고 절대 URL을 통해 명시적으로 지정 된 위치에 상대적입니다 [연결](../../../ado/reference/ado-api/connection-object-ado.md) 개체입니다.  
  
> [!NOTE]
>  Http 체계를 사용 하 여 Url은 자동으로 호출 합니다 [Microsoft OLE DB Provider for Internet Publishing](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-internet-publishing.md)합니다. 자세한 내용은 [절대 및 상대 Url](../../../ado/guide/data/absolute-and-relative-urls.md)합니다.  
  
## <a name="applies-to"></a>적용 대상  
 [명령 개체(ADO)](../../../ado/reference/ado-api/command-object-ado.md)  
  
## <a name="see-also"></a>관련 항목  
 [ActiveConnection, CommandText, CommandTimeout, CommandType, 크기 및 방향 속성 예제 (VB)](../../../ado/reference/ado-api/activeconnection-commandtext-commandtimeout-commandtype-size-example-vb.md)   
 [ActiveConnection, CommandText, CommandTimeout, CommandType, 크기 및 방향 속성 예제 (VC + +)](../../../ado/reference/ado-api/activeconnection-commandtext-commandtimeout-commandtype-size-example-vc.md)   
 [Requery 메서드](../../../ado/reference/ado-api/requery-method.md)   
 [ActiveConnection, CommandText, CommandTimeout, CommandType, 크기 및 방향 속성 예제 (JScript)](../../../ado/reference/ado-api/activeconnection-commandtext-timeout-type-size-example-jscript.md)
