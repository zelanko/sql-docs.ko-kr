---
title: LocalDB에 대 한 SQL Server Native Client 지원 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
ms.assetid: 127569d1-a9f7-49bf-a561-c084986a8871
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: 503bae580d2bacffbd143a1b4530f83b7c81a269
ms.sourcegitcommit: b72c9fc9436c44c6a21fd96223c73bf94706c06b
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/01/2020
ms.locfileid: "82707221"
---
# <a name="sql-server-native-client-support-for-localdb"></a>LocalDB에 대한 SQL Server Native Client 지원
  [!INCLUDE[ssSQL11](../../../includes/sssql11-md.md)]부터는 LocalDB라고 부르는 SQL Server의 경량 버전을 사용할 수 있습니다. 이 항목에서는 LocalDB 인스턴스의 데이터베이스에 연결하는 방법에 대해 설명합니다.  
  
## <a name="remarks"></a>설명  
 LocalDB 설치 및 LocalDB 인스턴스 구성 방법을 포함하여 LocalDB에 대한 자세한 내용은 다음을 참조하십시오.  
  
-   [SQL Server Express LocalDB 참조](../../sql-server-express-localdb-reference.md)  
  
-   [SQL Server 2014 Express LocalDB](../../../database-engine/configure-windows/sql-server-2016-express-localdb.md)  
  
 요약하자면, LocalDB를 통해 다음과 같은 기능을 수행할 수 있습니다.  
  
-   `sqllocaldb.exe i`를 사용하여 기본 인스턴스의 이름을 확인할 수 있습니다.  
  
-   `AttachDBFilename` 연결 문자열 키워드를 사용하여 서버가 연결해야 하는 데이터베이스 파일을 지정할 수 있습니다. 를 사용 하는 경우 데이터베이스 연결 문자열 키워드를 사용 하 여 `AttachDBFilename` 데이터베이스 이름을 **Database** 지정 하지 않으면 응용 프로그램이 닫힐 때 LocalDB 인스턴스에서 데이터베이스가 제거 됩니다.  
  
-   연결 문자열에 LocalDB 인스턴스를 지정합니다.  
  
```  
SERVER=(localdb)\v11.0  
```  
  
 필요한 경우 sqllocaldb.exe를 사용하여 LocalDB 인스턴스를 만들 수 있습니다. 또한 sqlcmd.exe를 사용하여 LocalDB 인스턴스에서 데이터베이스를 추가하고 수정할 수 있습니다. `sqlcmd -S (localdb)\v11.0`)을 입력합니다.  
  
## <a name="see-also"></a>참고 항목  
 [SQL Server Native Client 기능](sql-server-native-client-features.md)  
  
  
