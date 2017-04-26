---
title: "2단원: 스냅숏 폴더 준비 | Microsoft 문서"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
applies_to:
- SQL Server 2016
helpviewer_keywords:
- replication [SQL Server], tutorials
ms.assetid: f286cde9-c0d0-43ef-b7ba-53c3cbb8906c
caps.latest.revision: 20
author: BYHAM
ms.author: rickbyh
manager: jhubbard
translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: f9b63fa28f53724adce16bedda14e11cd3a750b8
ms.lasthandoff: 04/11/2017

---
# <a name="lesson-2-preparing-the-snapshot-folder"></a>2단원: 스냅숏 폴더 준비
이 단원에서는 게시 스냅숏을 만들고 저장하는 데 사용되는 스냅숏 폴더를 구성하는 방법을 배웁니다.  
  
### <a name="to-create-a-share-for-the-snapshot-folder-and-assign-permissions"></a>스냅숏 폴더에 대한 공유를 만들고 사용 권한을 할당하려면  
  
1.  Windows 탐색기에서 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터 폴더로 이동합니다. 기본 위치는 C:\Program Files\Microsoft SQL Server\MSSQL.X\MSSQL\Data입니다.  
  
2.  **repldata**라는 새 폴더를 만듭니다.  
  
3.  이 폴더를 마우스 오른쪽 단추로 클릭한 다음 **속성**을 클릭합니다.  
  
4.  **repldata 속성** 대화 상자의 **공유** 탭에서 **공유**를 클릭합니다.  
  
5.  **파일 공유** 대화 상자에서 **공유**를 클릭한 다음 **완료**를 클릭합니다.  
  
6.  **보안** 탭에서 **편집**을 클릭합니다.  
  
7.  **권한** 대화 상자에서 **추가**를 클릭합니다. **사용자, 컴퓨터, 서비스 계정 또는 그룹 선택** 입력란에 1단원에서 만든 스냅숏 에이전트 계정 이름을 \<*Machine_Name>***\repl_snapshot**으로 입력합니다. 여기서 \<*Machine_Name>*은 게시자의 이름입니다. **이름 확인**을 클릭한 다음 **확인**을 클릭합니다.  
  
8.  이전 단계를 반복하여 배포 에이전트에 대한 사용 권한을 \<*Machine_Name>***\repl_distribution**으로, 병합 에이전트에 대한 사용 권한을 \<*Machine_Name>***\repl_merge**로 추가합니다.  
  
9. 다음 사용 권한이 허용되는지 확인합니다.  
  
    -   repl_snapshot - 모든 권한  
  
    -   repl_distribution - 읽기  
  
    -   repl_merge - 읽기  
  
10. **확인** 을 클릭하여 **repldata 속성** 대화 상자를 닫고 repldata 공유를 만듭니다.  
  
## <a name="next-steps"></a>다음 단계  
스냅숏 폴더에 대한 공유를 성공적으로 구성했습니다. 다음 단원에서는 배포를 구성합니다. [3단원: 배포 구성](../../relational-databases/replication/lesson-3-configuring-distribution.md)을 참조하세요.  
  
## <a name="see-also"></a>관련 항목:  
[스냅숏 폴더 보안 설정](../../relational-databases/replication/security/secure-the-snapshot-folder.md)  
  
  
  

