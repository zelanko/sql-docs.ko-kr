---
description: ADOX 열거 상수
title: ADOX 열거 상수 | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- enumerated constants [ADOX]
ms.assetid: 9d91f511-d46f-44ef-97ef-77bf93836186
author: rothja
ms.author: jroth
ms.openlocfilehash: 1def9c0445551376aec56c36c554b9c74b15c02f
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/27/2020
ms.locfileid: "88985714"
---
# <a name="adox-enumerated-constants"></a>ADOX 열거 상수
디버깅을 지원 하기 위해 ADOX 열거 상수에는 각 상수에 대 한 값이 나열 됩니다. 그러나이 값은 전적으로 advise 이며 ADOX의 한 릴리스에서 다른 릴리스로 변경 될 수 있습니다. 코드는 열거 상수의 실제 값이 아닌 이름에만 의존 해야 합니다.  
  
 다음 열거 상수가 정의 됩니다.  
  
|열거형|설명|  
|-----------------|-----------------|  
|[ActionEnum](./actionenum.md)|**SetPermissions** 가 호출 될 때 수행할 동작의 유형을 지정 합니다.|  
|[AllowNullsEnum](./allownullsenum.md)|Null 값이 있는 레코드를 인덱싱할 지 여부를 지정 합니다.|  
|[ColumnAttributesEnum](./columnattributesenum.md)|**열의**특성을 지정 합니다.|  
|[DataTypeEnum](../ado-api/datatypeenum.md)|**필드**, **매개 변수**또는 **속성**의 데이터 형식을 지정 합니다.|  
|[InheritTypeEnum](./inherittypeenum.md)|개체가 **SetPermissions**로 설정 된 사용 권한을 상속 하는 방법을 지정 합니다.|  
|[KeyTypeEnum](./keytypeenum.md)|기본, 외부 또는 고유 **키**의 유형을 지정 합니다.|  
|[ObjectTypeEnum](./objecttypeenum.md)|사용 권한이 나 소유권을 설정할 데이터베이스 개체의 유형을 지정 합니다.|  
|[RightsEnum](./rightsenum.md)|개체의 그룹 또는 사용자에 대 한 권한 또는 사용 권한을 지정 합니다.|  
|[RuleEnum](./ruleenum.md)|**키** 를 삭제할 때 따라야 하는 규칙을 지정 합니다.|  
|[SortOrderEnum](./sortorderenum.md)|인덱싱된 열에 대 한 정렬 순서를 지정 합니다.|  
  
## <a name="see-also"></a>참고 항목  
 [ADOX API 참조](./adox-object-model.md?view=sql-server-ver15)   
 [데이터 정의 언어 및 보안을 위한 ADO 확장(ADOX)](../../guide/extensions/ado-extensions-for-data-definition-language-and-security-adox.md)