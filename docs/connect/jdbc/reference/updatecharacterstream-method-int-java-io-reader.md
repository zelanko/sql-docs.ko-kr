---
description: updateCharacterStream 메서드(int, java.io.Reader)
title: updateCharacterStream 메서드(int, java.io.Reader) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 4dddf885-0482-4776-8e9a-69f6c6270931
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 8f4d8d4ae626fada30b9dacda009ddfe5a2553fe
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88354019"
---
# <a name="updatecharacterstream-method-int-javaioreader"></a>updateCharacterStream 메서드(int, java.io.Reader)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  지정된 열을 문자 스트림 값으로 업데이트합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
public void updateCharacterStream(int columnIndex,  
                                  java.io.Reader x)  
```  
  
#### <a name="parameters"></a>매개 변수  
 *columnIndex*  
  
 열 인덱스를 나타내는 **int**입니다.  
  
 *x*  
  
 Reader 개체입니다.  
  
## <a name="exceptions"></a>예외  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>설명  
 이 updateCharacterStream 메서드는 java.sql.ResultSet 인터페이스의 updateCharacterStream 메서드에 의해 지정됩니다.  
  
 이 메서드는 판독기 개체의 유니코드 문자를 선택된 텍스트 및 이진 열에 전달합니다. 여기에는 모든 텍스트 열과 **binary**, **varbinary**, **varbinary(max)** , **image** 및 **xml** 열이 포함되지만 **udt** 열은 포함되지 않습니다.  
  
 **image**, **text** 및 **ntext**[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 데이터 형식에 이 메서드를 사용할 경우 성능이 저하될 수 있습니다.  
  
## <a name="see-also"></a>참고 항목  
 [updateCharacterStream 메서드&#40;SQLServerResultSet&#41;](../../../connect/jdbc/reference/updatecharacterstream-method-sqlserverresultset.md)   
 [SQLServerResultSet 멤버](../../../connect/jdbc/reference/sqlserverresultset-members.md)   
 [SQLServerResultSet 클래스](../../../connect/jdbc/reference/sqlserverresultset-class.md)  
  
  
