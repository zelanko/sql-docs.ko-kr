---
title: "setURL 메서드 (SQLServerDataSource) | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
apiname:
- SQLServerDataSource.setURL
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: bea70100-ac98-4625-8748-ef7cc0b111ea
caps.latest.revision: 10
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: dd1f100fcf00678741675c113512eb95a3484368
ms.contentlocale: ko-kr
ms.lasthandoff: 09/09/2017

---
# <a name="seturl-method-sqlserverdatasource"></a>setURL 메서드(SQLServerDataSource)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  데이터 원본에 연결하는 데 사용되는 URL을 설정합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
public void setURL(java.lang.String url)  
```  
  
#### <a name="parameters"></a>매개 변수  
 *url*  
  
 A **문자열** URL이 들어 있는입니다.  
  
## <a name="remarks"></a>주의  
 보안상의 이유로 setURL 메서드에 제공 된 URL에 암호를 포함 하지 말아야 합니다. 이는 타사 Java 응용 프로그램 서버가 URL 속성에 설정된 값을 데이터 원본 구성 사용자 인터페이스에 표시하는 경우가 매우 많기 때문입니다. 대신를 사용 하 여는 [setPassword](../../../connect/jdbc/reference/setpassword-method-sqlserverdatasource.md) 암호 값을 설정 하는 메서드. 데이터 원본에 설정된 암호는 Java 응용 프로그램 서버가 구성 사용자 인터페이스에 표시하지 않습니다.  
  
> [!NOTE]  
>  SetURL 메서드 호출 하기 전에 호출 되지 않으면는 [getURL](../../../connect/jdbc/reference/geturl-method-sqlserverdatasource.md) getURL 메서드를 기본값인을 반환 "jdbc:sqlserver: / /"입니다.  
  
## <a name="see-also"></a>관련 항목:  
 [SQLServerDataSource 멤버](../../../connect/jdbc/reference/sqlserverdatasource-members.md)   
 [SQLServerDataSource 클래스](../../../connect/jdbc/reference/sqlserverdatasource-class.md)  
  
  
