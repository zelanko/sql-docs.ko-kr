---
title: "ADO Java 클래스 래퍼 | Microsoft Docs"
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: guide
ms.technology: drivers
ms.custom: 
ms.date: 02/15/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords: class wrappers [ADO]
ms.assetid: 1fc09dc1-9e32-412e-9f43-b8eb8bb483ca
caps.latest.revision: "10"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 44a9b6f6eeedd29bf8dacd69e07bc0d64c7161c8
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/17/2017
---
# <a name="ado-java-class-wrappers"></a>ADO Java 클래스 래퍼
이 코드는 ADO의 인스턴스를 선언 [레코드 집합](../../../ado/reference/ado-api/recordset-object-ado.md) 클래스 래퍼를 모두 동일한 코드 줄에 초기화 합니다. 또한 각 인수에 변수를 선언는 [열려](../../../ado/reference/ado-api/open-method-ado-recordset.md) 메서드, 특히 [LockType](../../../ado/reference/ado-api/locktype-property-ado.md) 및 [모두](../../../ado/reference/ado-api/cursortype-property-ado.md) (Java를 지원 하지 않으므로 열거 형식)입니다. 열고 닫습니다는 **레코드 집합** 개체입니다. 변수를 사용 하지 않는 개체의 체계적이 고 일시적인 출시를 수행 하는 Java 때 해제로 예약을 NULL로 단순히 Rs1를 설정 합니다.  
  
```  
public static void main( String args[])  
{  
   msado15._Recordset   Rs1 = new msado15.Recordset();  
   Variant Source     = new Variant( "SELECT * FROM Authors" );  
   Variant Connect    = new Variant( "DSN=AdoDemo;UID=admin;PWD=;" );  
   int     LockType   = msado15.CursorTypeEnum.adOpenForwardOnly;  
   int     CursorType = msado15.LockTypeEnum.adLockReadOnly;  
   int     Options    = -1;  
  
   Rs1.Open( Source, Connect, LockType,  CursorType, Options );  
   Rs1.Close();  
   Rs1 = null;  
  
   System.out.println( "Success!\n" );  
}  
```  
  
## <a name="see-also"></a>관련 항목:  
 [Java용 Microsoft SDK 사용](../../../ado/guide/appendixes/using-the-microsoft-sdk-for-java.md)
