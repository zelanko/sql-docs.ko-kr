---
title: "Hadoop 연결 관리자 | Microsoft Docs"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-non-specified
ms.prod_service: integration-services
ms.service: 
ms.component: connection-manager
ms.reviewer: 
ms.suite: sql
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sql13.ssis.designer.hadoopconn.f1
ms.assetid: 8bb15b97-9827-46bc-aca6-068534ab18c4
caps.latest.revision: 7
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 79b0782d0d01733f10310f1eaac611fc688dbf21
ms.contentlocale: ko-kr
ms.lasthandoff: 08/03/2017

---
# <a name="hadoop-connection-manager"></a>Hadoop 연결 관리자
  SSIS 패키지는 Hadoop 연결 관리자를 통해 속성에 대해 지정된 값을 사용하여 Hadoop 클러스터에 연결할 수 있습니다.  
  
## <a name="configure-the-hadoop-connection-manager"></a>Hadoop 연결 관리자 구성  
  
1.  **SSIS 연결 관리자 추가** 대화 상자에서 **Hadoop**을 선택하고 **추가**를 클릭합니다. **Hadoop 연결 관리자 편집기** 대화 상자가 열립니다.  
  
2.  왼쪽 창에서 **WebHCat** 또는 **WebHDFS** 탭을 선택하여 관련 Hadoop 클러스터 정보를 구성합니다.  
  
3.  Hadoop에서 하이브 또는 Pig 작업을 호출하기 위해 **WebHCat** 을 사용하도록 설정하는 경우에는 다음 단계를 수행합니다.  
  
    1.  **WebHCat 호스트**에는 WebHCat 서비스를 호스트하는 서버를 입력합니다.  
  
    2.  **WebHCat 포트**에는 WebHCat 서비스의 포트(기본값: 50111)를 입력합니다.  
  
    3.  WebHCat 서비스에 액세스하는 데 사용할 **인증** 방법을 선택합니다. 사용 가능한 값은 **기본** 및 **Kerberos**입니다.  
  
         ![Hadoop 연결 관리자 편집기는 기본 인증으로](../../integration-services/connection-manager/media/hadoop-cm-basic.png "기본 인증과 함께 Hadoop 연결 관리자 편집기")  
  
         ![Kerberos 인증 Hadoop 연결 관리자 편집기](../../integration-services/connection-manager/media/hadoop-cm-kerberos.png "Kerberos 인증 Hadoop 연결 관리자 편집기")  
  
    4.  **WebHCat 사용자**에는 WebHCat 액세스 권한이 있는 **사용자** 를 입력합니다.  
  
    5.  **Kerberos** 인증을 선택하는 경우 사용자의 **암호** 및 **도메인**을 입력합니다.  
  
4.  HDFS에서/HDFS로 데이터를 복사하기 위해 **WebHDFS** 를 사용하도록 설정하는 경우에는 다음 단계를 수행합니다.  
  
    1.  **WebHDFS 호스트**에는 WebHDFS 서비스를 호스트하는 서버를 입력합니다.  
  
    2.  **WebHDFS 포트**에는 WebHDFS 서비스의 포트(기본값: 50070)를 입력합니다.  
  
    3.  WebHDFS 서비스에 액세스하는 데 사용할 **인증** 방법을 선택합니다. 사용 가능한 값은 **기본** 및 **Kerberos**입니다.  
  
    4.  **WebHDFS 사용자**에는 HDFS 액세스 권한이 있는 사용자를 입력합니다.  
  
    5.  **Kerberos** 인증을 선택하는 경우 사용자의 **암호** 및 **도메인**을 입력합니다.  
  
5.  **연결 테스트** 를 클릭하여 연결을 테스트합니다. 사용하도록 설정한 연결만 테스트합니다.  
  
6.  **확인** 을 클릭하여 대화 상자를 닫습니다.  
  
## <a name="see-also"></a>관련 항목:  
 [Hadoop 하이브 태스크](../../integration-services/control-flow/hadoop-hive-task.md)   
 [Hadoop Pig 작업](../../integration-services/control-flow/hadoop-pig-task.md)   
 [Hadoop 파일 시스템 태스크](../../integration-services/control-flow/hadoop-file-system-task.md)  
  
  

