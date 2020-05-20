---
title: DefaultDatabase 속성 | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Connection15::DefaultDatabase
helpviewer_keywords:
- DefaultDatabase property
ms.assetid: 41e8a8dd-e69c-4a09-8736-93502e01961c
author: rothja
ms.author: jroth
ms.openlocfilehash: 5a68a41985515e63e6e8520c30fc662c69e1ced6
ms.sourcegitcommit: 6037fb1f1a5ddd933017029eda5f5c281939100c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/04/2020
ms.locfileid: "82757449"
---
# <a name="defaultdatabase-property"></a>DefaultDatabase 속성
[연결](../../../ado/reference/ado-api/connection-object-ado.md) 개체에 대 한 기본 데이터베이스를 나타냅니다.  
  
## <a name="settings-and-return-values"></a>설정 및 반환 값  
 공급자에서 사용할 수 있는 데이터베이스의 이름으로 계산 되는 **문자열** 값을 설정 하거나 반환 합니다.  
  
## <a name="remarks"></a>설명  
 **Defaultdatabase** 속성을 사용 하 여 특정 **연결** 개체에 대 한 기본 데이터베이스의 이름을 설정 하거나 반환할 수 있습니다.  
  
 기본 데이터베이스가 있는 경우 SQL 문자열은 정규화 되지 않은 구문을 사용 하 여 해당 데이터베이스의 개체에 액세스할 수 있습니다. **Defaultdatabase** 속성에 지정 된 개체 이외의 데이터베이스에 있는 개체에 액세스 하려면 원하는 데이터베이스 이름으로 개체 이름을 한정 해야 합니다. 연결 되 면 공급자는 기본 데이터베이스 정보를 **defaultdatabase** 속성에 기록 합니다. 일부 공급자는 연결당 하나의 데이터베이스만 허용 하며,이 경우 **defaultdatabase** 속성을 변경할 수 없습니다.  
  
 일부 데이터 원본 및 공급자는이 기능을 지원 하지 않을 수 있으며 오류 또는 빈 문자열을 반환할 수 있습니다.  
  
> [!NOTE]
>  **원격 데이터 서비스 사용** 클라이언트 쪽 **연결** 개체에서는이 속성을 사용할 수 없습니다.  
  
## <a name="applies-to"></a>적용 대상  
 [연결 개체(ADO)](../../../ado/reference/ado-api/connection-object-ado.md)  
  
## <a name="see-also"></a>참고 항목  
 [Provider 및 DefaultDatabase 속성 예제 (VB)](../../../ado/reference/ado-api/provider-and-defaultdatabase-properties-example-vb.md)   
 [Provider 및 DefaultDatabase 속성 예제(VC++)](../../../ado/reference/ado-api/provider-and-defaultdatabase-properties-example-vc.md)   
