---
description: CommandStream 속성(ADO)
title: CommandStream 속성 (ADO) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- _Command::CommandStream
helpviewer_keywords:
- CommandStream property [ADO]
ms.assetid: f78f61b6-87e0-48dc-961e-83d0e20da58e
author: rothja
ms.author: jroth
ms.openlocfilehash: 20b52a91429e2db6478aab36f2db5928bc2d30f5
ms.sourcegitcommit: 7345e4f05d6c06e1bcd73747a4a47873b3f3251f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/24/2020
ms.locfileid: "88776152"
---
# <a name="commandstream-property-ado"></a>CommandStream 속성(ADO)
[명령](./command-object-ado.md) 개체에 대 한 입력으로 사용 되는 스트림을 나타냅니다.  
  
## <a name="settings-and-return-values"></a>설정 및 반환 값  
 **명령** 개체에 대 한 입력으로 사용 되는 스트림을 설정 하거나 반환 합니다. 이 스트림의 형식은 공급자별로 다릅니다. 자세한 내용은 공급자 설명서를 참조 하세요. 이 속성은 **명령**입력에 대 한 문자열을 지정 하는 데 사용 되는 [CommandText](./commandtext-property-ado.md) 속성과 유사 합니다.  
  
## <a name="remarks"></a>설명  
 **Commandstream** 및 **CommandText** 는 함께 사용할 수 없습니다. 사용자가 **Commandstream** 속성을 설정 하는 경우 **CommandText** 속성은 빈 문자열 ("")로 설정 됩니다. 사용자가 **CommandText** 속성을 설정 하는 경우 **Commandstream** 속성은 **Nothing**으로 설정 됩니다.  
  
 명령의 동작입니다. **Refresh** 및 **command. Prepare** 메서드는 공급자에 의해 정의 됩니다. 스트림의 매개 변수 값을 새로 고칠 수 없습니다.  
  
 입력 스트림은 **명령의**원본을 반환 하는 다른 ADO 개체에 사용할 수 없습니다. 예를 들어 [레코드 집합](./recordset-object-ado.md) 의 [소스가](./source-property-ado-recordset.md) stream을 입력으로 포함 하는 **Command** 개체로 설정 된 경우에는 **레코드 집합. Source** 는 **commandstream** 속성의 스트림 콘텐츠 대신 빈 문자열 ("")이 포함 된 **CommandText** 속성을 계속 반환 합니다.  
  
 **Commandstream**에 지정 된 대로 명령 스트림을 사용할 때 [CommandType](./commandtype-property-ado.md) 속성의 유효한 [CommandTypeEnum](./commandtypeenum.md) 값은 **adcmdtext** 및 **adcmdtext**입니다. 다른 값을 사용하면 오류가 발생합니다.  
  
## <a name="applies-to"></a>적용 대상  
 [명령 개체(ADO)](./command-object-ado.md)  
  
## <a name="see-also"></a>참고 항목  
 [CommandText 속성 (ADO)](./commandtext-property-ado.md)   
 [언어 속성](./dialect-property.md)   
 [CommandTypeEnum](./commandtypeenum.md)