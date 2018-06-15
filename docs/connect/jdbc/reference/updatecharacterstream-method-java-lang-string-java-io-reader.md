---
title: updateCharacterStream 메서드 (java.lang.String, java.io.Reader) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: a8ec22a9-4bbd-4759-9f21-957304ef3a5e
caps.latest.revision: 17
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: f9c755a658b0a63966a2db4be4e55b09b1004a0a
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
ms.locfileid: "32850598"
---
# <a name="updatecharacterstream-method-javalangstring-javaioreader"></a>updateCharacterStream 메서드(java.lang.String, java.io.Reader)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  지정된 열을 문자 스트림 값으로 업데이트합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
public void updateCharacterStream(java.lang.String columnLabel,  
                                  java.io.Reader reader)  
```  
  
#### <a name="parameters"></a>매개 변수  
 *columnLabel*  
  
 A **문자열** 열 레이블이 들어 있는입니다.  
  
 *판독기*  
  
 판독기 개체입니다.  
  
## <a name="exceptions"></a>예외  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>주의  
 이 updateCharacterStream 메서드는 java.sql.ResultSet 인터페이스의 updateCharacterStream 메서드에 의해 지정 됩니다.  
  
 이 메서드는 선택한 텍스트 및 이진 열에 판독기 개체에서 유니코드 문자를 전달합니다. 이 모든 텍스트 열을 포함 하 고 **이진**, **varbinary**, **varbinary (max)**, **이미지**, 및 **xml**열 아닌 **udt** 열입니다.  
  
 이 메서드를 사용 하는 **이미지**, **텍스트**, 및 **ntext** [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] 데이터 형식에는 성능 저하 될 수 있습니다.  
  
## <a name="see-also"></a>관련 항목:  
 [updateCharacterStream 메서드 &#40;SQLServerResultSet&#41;](../../../connect/jdbc/reference/updatecharacterstream-method-sqlserverresultset.md)   
 [SQLServerResultSet 멤버](../../../connect/jdbc/reference/sqlserverresultset-members.md)   
 [SQLServerResultSet 클래스](../../../connect/jdbc/reference/sqlserverresultset-class.md)  
  
  
