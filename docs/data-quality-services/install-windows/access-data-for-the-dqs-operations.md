---
title: "DQS 작업을 위해 데이터 액세스 | Microsoft Docs"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- data-quality-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 88dfb9ea-6321-4eaf-b9e4-45d36ef048f6
caps.latest.revision: 15
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.translationtype: HT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: a03861b1706667657461ecf95196fc6cb3501d2f
ms.contentlocale: ko-kr
ms.lasthandoff: 09/01/2017

---
# <a name="access-data-for-the-dqs-operations"></a>DQS 작업을 위해 데이터 액세스
  [!INCLUDE[ssDQSnoversion](../../includes/ssdqsnoversion-md.md)] (DQS) 작업에 원본 데이터를 사용하고 처리된 데이터를 내보내려면 다음 중 하나를 수행할 수 있습니다.  
  
-   원본 데이터를 DQS_STAGING_DATA 데이터베이스의 테이블/뷰로 복사한 다음 이를 DQS 작업에 사용합니다. 처리된 데이터를 DQS_STAGING_DATA 데이터베이스의 새 테이블로 내보낼 수도 있습니다. 이렇게 하려면 Windows 사용자 계정에 DQS_STAGING_DATA 데이터베이스에 대한 읽기/쓰기 액세스 권한을 부여해야 합니다.  
  
-   사용자 데이터베이스를 DQS 작업의 원본 데이터 및 처리된 데이터의 내보내기 대상으로 사용합니다. 이렇게 하려면 사용자 데이터베이스가 데이터 품질 서버 데이터베이스와 동일한 SQL Server 인스턴스에 있어야 합니다. 그렇지 않으면 데이터 품질 클라이언트에서 해당 데이터베이스를 DQS 작업에 사용할 수 없습니다. 또한 일치하는 결과는 2단계로 내보내지므로 일치하는 결과를 내보내려면 Windows 사용자 계정에 DQS_STAGING_DATA 데이터베이스에 대한 읽기 권한을 부여해야 합니다. 먼저 일치하는 결과를 DQS_STAGING_DATA 데이터베이스의 임시 표로 내보낸 다음 대상 데이터베이스의 표로 이동합니다.  
  
## <a name="prerequisites"></a>필수 구성 요소  
  
-   DQSInstaller.exe 파일을 실행하여 [!INCLUDE[ssDQSServer](../../includes/ssdqsserver-md.md)] 설치를 완료해야 합니다. 자세한 내용은 [DQSInstaller.exe를 실행하여 Data Quality 서버 설치 완료](../../data-quality-services/install-windows/run-dqsinstaller-exe-to-complete-data-quality-server-installation.md)를 참조하세요.  
  
-   데이터베이스에서 SQL 로그인에 대한 액세스 권한을 부여/수정하려면 Windows 사용자 계정은 데이터베이스 엔진 인스턴스에서 적절한 고정 서버 역할(예: securityadmin, serveradmin 또는 sysadmin)의 멤버여야 합니다.  
  
### <a name="to-grant-readwrite-access-to-a-user-on-the-dqsstagingdata-database"></a>사용자에게 DQS_STAGING_DATA 데이터베이스에 대한 읽기/쓰기 액세스 권한을 부여하려면  
  
1.  Microsoft SQL Server Management Studio를 시작합니다.  
  
2.  Microsoft SQL Server Management Studio에서 해당 SQL Server 인스턴스를 확장하고 **보안**을 확장한 다음 **로그인**을 확장합니다.  
  
3.  SQL 로그인을 마우스 오른쪽 단추로 클릭하고 **속성**을 클릭합니다.  
  
4.  **로그인 속성** 대화 상자의 왼쪽 창에서 **사용자 매핑** 페이지를 클릭합니다.  
  
5.  오른쪽 창에서 **DQS_STAGING_DATA** 데이터베이스에 대한 **매핑** 열 아래의 확인란을 선택한 후 **데이터베이스 역할 멤버 자격: DQS_STAGING_DATA** 창에서 다음 역할을 선택합니다.  
  
    -   **db_datareader**: 테이블/뷰에서 데이터를 읽습니다.  
  
    -   **db_datawriter**: 테이블에서 데이터를 추가, 삭제 또는 변경합니다.  
  
    -   **db_ddladmin**: 테이블/뷰를 만들기, 수정 또는 삭제합니다.  
  
6.  **로그인 속성** 대화 상자에서 **확인** 을 클릭하여 변경 내용을 적용합니다.  
  
## <a name="next-steps"></a>다음 단계  
 DQS 작업을 위한 데이터 원본으로 데이터베이스에 액세스하는 DQS 작업을 수행한 다음 처리된 데이터를 데이터베이스로 내보냅니다.  
  
## <a name="see-also"></a>참고 항목  
 [Data Quality Services 설치](../../data-quality-services/install-windows/install-data-quality-services.md)  
  
  
