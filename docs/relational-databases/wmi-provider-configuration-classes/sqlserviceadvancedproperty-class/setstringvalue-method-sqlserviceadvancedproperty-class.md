---
title: SetStringValue 메서드 (SqlServiceAdvancedProperty 클래스) | Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: wmi
ms.topic: reference
apiname:
- SetStringValue Method (SqlServiceAdvancedProperty Class )
apilocation:
- sqlmgmproviderxpsp2up.mof
apitype: MOFDef
helpviewer_keywords:
- SetStringValue method
ms.assetid: a02d05f6-1072-4709-9ecc-e23e51c8c898
author: CarlRabeler
ms.author: carlrab
manager: craigg
ms.openlocfilehash: aa776b9b87d6742d530d87f08f00e7ac868a0788
ms.sourcegitcommit: 9c6a37175296144464ffea815f371c024fce7032
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/15/2018
ms.locfileid: "51675872"
---
# <a name="setstringvalue-method-sqlserviceadvancedproperty-class-"></a>SetStringValue 메서드(SqlServiceAdvancedProperty 클래스)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]
  속성의 문자열 값을 설정합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
object.SetStringValue(StrValue)  
```  
  
## <a name="parts"></a>부분  
 *object*  
 고급 속성을 나타내는 [SqlServiceAdvancedProperty 클래스](../../../relational-databases/wmi-provider-configuration-classes/sqlserviceadvancedproperty-class/sqlserviceadvancedproperty-class.md) 개체입니다.  
  
#### <a name="parameters"></a>매개 변수  
  
|매개 변수|설명|  
|---------------|-----------------|  
|*strValue*|고급 속성의 값을 지정하는 문자열 값입니다.|  
  
## <a name="property-valuereturn-value"></a>속성 값/반환 값  
 **uint32** 값으로, 0은 서비스가 수정되었음을 나타내고 1은 요청이 지원되지 않음을 나타내며 다른 모든 숫자는 오류를 나타냅니다.  
  
## <a name="remarks"></a>Remarks  
 속성 값 형식 이어야 합니다 **문자열** 속성 문자열 값을 설정 하는 일을 할 수 있습니다.  
  
## <a name="see-also"></a>관련 항목  
 [서비스 시작 및 중지](https://technet.microsoft.com/library/ms174886\(v=sql.105\).aspx)  
  
  
