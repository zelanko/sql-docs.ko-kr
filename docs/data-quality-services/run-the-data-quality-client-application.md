---
title: Data Quality Client 응용 프로그램 실행 | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: data-quality-services
ms.reviewer: ''
ms.technology:
- data-quality-services
ms.topic: conceptual
f1_keywords:
- sql13.dqs.browseforservers.f1
- sql13.dqs.connecttoserver.f1
ms.assetid: 0b2aa202-7ab2-4c9d-b0f1-802588053a1e
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 9cb3fd865f2e26addacd74a949f79ccfc6ba463c
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47736501"
---
# <a name="run-the-data-quality-client-application"></a>데이터 품질 클라이언트 응용 프로그램 실행

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

  [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)]을(를) 실행하고 [!INCLUDE[ssDQSServer](../includes/ssdqsserver-md.md)]에 로그온합니다.  
  
##  <a name="BeforeYouBegin"></a> 시작하기 전에  
  
###  <a name="Prerequisites"></a> 사전 요구 사항  
 DQSInstaller.exe 파일을 실행하여 [!INCLUDE[ssDQSServer](../includes/ssdqsserver-md.md)] 설치를 완료해야 합니다. 자세한 내용은 [DQSInstaller.exe를 실행하여 Data Quality 서버 설치 완료](../data-quality-services/install-windows/run-dqsinstaller-exe-to-complete-data-quality-server-installation.md)를 참조하세요.  
  
###  <a name="Security"></a> 보안  
  
####  <a name="Permissions"></a> Permissions  
 DQS_MAIN 데이터베이스에 대해 세 가지 DQS 역할(dqs_adminstrator, dqs_kb_editor 또는 dqs_kb_operator) 중 하나가 있어야 [!INCLUDE[ssDQSServer](../includes/ssdqsserver-md.md)]에 로그온할 수 있습니다.  
  
##  <a name="Run"></a> Data Quality 클라이언트 실행  
 설치된 컴퓨터에서 [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)] 를 실행하려면 다음과 같이 진행합니다.  
  
1.  **시작**을 클릭하고 **모든 프로그램**을 가리킨 다음 **[!INCLUDE[ssCurrent](../includes/sscurrent-md.md)]**, **Data Quality Services**, **Data Quality 클라이언트**를 차례로 클릭합니다.  
  
2.  **서버에 연결** 대화 상자에서  
  
    1.  [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)] 응용 프로그램을 연결할 서버를 지정합니다. **(로컬)** 을 선택하여 로컬 컴퓨터의 [!INCLUDE[ssDQSServer](../includes/ssdqsserver-md.md)] 에 연결할 수 있습니다. 아래쪽 화살표를 클릭하고 **\<네트워크에서 추가 서버 찾아보기>** 를 선택하여 다른 서버에 연결하거나 이름에 따라 로컬 서버에 연결할 수도 있습니다. **서버 찾아보기** 대화 상자가 표시됩니다. **로컬 서버** 탭이나 **네트워크 서버** 탭에서 서버를 선택할 수 있습니다.  
  
    2.  [!INCLUDE[ssDQSServer](../includes/ssdqsserver-md.md)] 와 [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)]사이의 데이터 전송을 암호화하려면 **옵션**을 클릭하고 **연결 암호화** 확인란을 선택합니다.  
  
3.  **연결**을 클릭합니다.  
  
 [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)] 홈 화면이 나타납니다. 자세한 내용은 [데이터 품질 클라이언트 홈 화면](../data-quality-services/data-quality-client-home-screen.md)을 참조하세요.  
  
  
