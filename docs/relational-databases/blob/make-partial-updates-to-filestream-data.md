---
title: FILESTREAM 데이터 부분 업데이트 | Microsoft 문서
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: database-engine
ms.component: blob
ms.reviewer: ''
ms.suite: sql
ms.technology:
- dbe-blob
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- FILESTREAM [SQL Server], FSCTL_SQL_FILESTREAM_FETCH_OLD_CONTENT
- FSCTL_SQL_FILESTREAM_FETCH_OLD_CONTENT
ms.assetid: d6f7661e-6c14-4d31-9541-4520ca0f82b2
caps.latest.revision: 16
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 492bb556378a21412240d0626ceb3ba91ad0acd9
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="make-partial-updates-to-filestream-data"></a>FILESTREAM 데이터 부분 업데이트
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  응용 프로그램은 FSCTL_SQL_FILESTREAM_FETCH_OLD_CONTENT를 사용하여 FILESTREAM BLOB 데이터를 부분적으로 업데이트합니다. [DeviceIoControl](http://go.microsoft.com/fwlink/?LinkId=105527) 함수는 [OpenSqlFilestream](../../relational-databases/blob/access-filestream-data-with-opensqlfilestream.md) 에서 반환된 핸들과 이 값을 FILESTREAM 드라이버로 전달합니다. 그런 다음 드라이버가 서버 쪽에서 현재 FILESTREAM 데이터를 복사하여 핸들에서 참조하는 파일에 붙여 넣습니다. 핸들이 작성된 후 응용 프로그램이 FSCTL_SQL_FILESTREAM_FETCH_OLD_CONTENT 값을 실행하면 마지막 쓰기 작업이 유지되고 핸들에 기록된 이전의 쓰기 작업은 손실됩니다.  
  
> [!NOTE]  
>  FILESTREAM은 원격 액세스를 위해 [SMB 프로토콜](http://go.microsoft.com/fwlink/?LinkId=112454) 을 사용합니다.  
  
## <a name="example"></a>예제  
 다음 예에서는 `FSCTL_SQL_FILESTREAM_FETCH_OLD_CONTENT` 값을 사용하여 삽입된 FILESTREAM BLOB의 부분 업데이트를 수행하는 방법을 보여 줍니다.  
  
> [!NOTE]  
>  이 예에서는 [FILESTREAM 사용 데이터베이스 만들기](../../relational-databases/blob/create-a-filestream-enabled-database.md) 및 [FILESTREAM 데이터 저장용 테이블 만들기](../../relational-databases/blob/create-a-table-for-storing-filestream-data.md)에서 만든 FILESTREAM 사용 데이터베이스 및 테이블이 필요합니다.  
  
 [!code-cpp[FILESTREAM#FS_CPP_FSCTL](../../relational-databases/blob/codesnippet/cpp/make-partial-updates-to-_1.cpp)]  
  
## <a name="see-also"></a>참고 항목  
 [OpenSqlFilestream을 사용하여 FILESTREAM 데이터 액세스](../../relational-databases/blob/access-filestream-data-with-opensqlfilestream.md)   
 [FILESTREAM 데이터용 클라이언트 응용 프로그램 만들기](../../relational-databases/blob/create-client-applications-for-filestream-data.md)  
  
  
