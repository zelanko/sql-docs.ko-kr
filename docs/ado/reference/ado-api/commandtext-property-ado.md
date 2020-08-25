---
description: CommandText 속성(ADO)
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
author: rothja
ms.author: jroth
ms.openlocfilehash: e23ae5bffca27d7ad9940fb4f03df81645094792
ms.sourcegitcommit: 7345e4f05d6c06e1bcd73747a4a47873b3f3251f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/24/2020
ms.locfileid: "88776122"
---
# <a name="commandtext-property-ado"></a>CommandText 속성(ADO)
공급자에 대해 실행할 명령의 텍스트를 나타냅니다.  
  
## <a name="settings-and-return-values"></a>설정 및 반환 값  
 SQL 문, 테이블 이름, 상대 URL 또는 저장 프로시저 호출과 같은 공급자 명령을 포함 하는 **문자열** 값을 가져오거나 설정 합니다. 기본값은 빈 문자열("")입니다.  
  
## <a name="remarks"></a>설명  
 **CommandText** 속성을 사용 하 여 [명령](./command-object-ado.md) 개체가 나타내는 명령의 텍스트를 설정 하거나 반환 합니다. 일반적으로이는 SQL 문이 되지만 저장 프로시저 호출과 같이 공급자가 인식 하는 다른 유형의 명령 문이 될 수도 있습니다. SQL 문은 공급자의 쿼리 프로세서에서 지 원하는 특정 언어 또는 버전 이어야 합니다.  
  
 **명령** 개체의 [준비](./prepared-property-ado.md) 된 속성이 **True** 로 설정 되어 있고 **명령** 개체가 열린 연결에 바인딩된 경우 **CommandText** 속성을 설정 하면 ADO에서 [Execute](./execute-method-ado-command.md) 또는 [open](./open-method-ado-connection.md) 메서드를 호출할 때 쿼리 (공급자에 의해 저장 된 쿼리의 컴파일된 형태)를 준비 합니다.  
  
 [CommandType](./commandtype-property-ado.md) 속성 설정에 따라 ADO는 **CommandText** 속성을 변경할 수 있습니다. 언제 든 지 **CommandText** 속성을 읽어 ADO에서 실행 중에 사용할 실제 명령 텍스트를 확인할 수 있습니다.  
  
 **CommandText** 속성을 사용 하 여 파일 또는 디렉터리와 같은 리소스를 지정 하는 상대 URL을 설정 하거나 반환 합니다. 리소스는 절대 URL로 명시적으로 지정 되거나 열린 [연결](./connection-object-ado.md) 개체에 의해 암시적으로 지정 된 위치에 상대적입니다.  
  
> [!NOTE]
>  Http 체계를 사용 하는 Url은 자동으로 [Microsoft OLE DB 공급자에 게 Internet 게시용](../../guide/appendixes/microsoft-ole-db-provider-for-internet-publishing.md)으로 호출 됩니다. 자세한 내용은 [절대 및 상대 url](../../guide/data/absolute-and-relative-urls.md)을 참조 하세요.  
  
## <a name="applies-to"></a>적용 대상  
 [명령 개체(ADO)](./command-object-ado.md)  
  
## <a name="see-also"></a>참고 항목  
 [ActiveConnection, CommandText, CommandTimeout, CommandType, Size 및 Direction 속성 예제 (VB)](./activeconnection-commandtext-commandtimeout-commandtype-size-example-vb.md)   
 [ActiveConnection, CommandText, CommandTimeout, CommandType, Size 및 Direction 속성 예제 (VC + +)](./activeconnection-commandtext-commandtimeout-commandtype-size-example-vc.md)   
 [Requery 메서드](./requery-method.md)   
 [ActiveConnection, CommandText, CommandTimeout, CommandType, Size 및 Direction 속성 예제 (JScript)](./activeconnection-commandtext-timeout-type-size-example-jscript.md)