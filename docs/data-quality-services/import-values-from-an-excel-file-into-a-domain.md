---
title: Excel 파일에서 도메인으로 값 가져오기 | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: data-quality-services
ms.reviewer: ''
ms.suite: sql
ms.technology:
- data-quality-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
f1_keywords:
- sql13.dqs.kb.importfailing.f1
- sql13.dqs.kb.importselect.f1
- sql13.dqs.kb.failingvalues.f1
ms.assetid: 04cde693-2043-477f-8417-fcc463ca7195
caps.latest.revision: 26
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: b2c08d8310e399a6b48e53f5e53ced3734f9af54
ms.sourcegitcommit: f16003fd1ca28b5e06d5700e730f681720006816
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/11/2018
ms.locfileid: "35310772"
---
# <a name="import-values-from-an-excel-file-into-a-domain"></a>Excel 파일에서 도메인으로 값 가져오기

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

  이 항목에서는 DQS( [!INCLUDE[ssDQSnoversion](../includes/ssdqsnoversion-md.md)] )에서 Excel 파일의 값을 도메인으로 가져오는 방법에 대해 설명합니다. Excel 파일을 사용하여 도메인 값을 [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)] 응용 프로그램으로 가져오면 기술 자료 생성 프로세스가 간소화되어 시간과 노력을 절감할 수 있습니다. 이 방법을 사용하면 Excel 파일이나 텍스트 파일로 올바른 데이터 값 목록을 가진 사용자가 해당 값을 도메인으로 가져올 수 있습니다. Excel 파일에서 도메인이나 기술 자료로 도메인 값을 가져올 수 있습니다. (기술 자료로 도메인 가져오기에 대한 자세한 내용은 [기술 자료 검색 시 Excel 파일에서 도메인 가져오기](../data-quality-services/import-domains-from-an-excel-file-in-knowledge-discovery.md)를 참조하세요.) Excel 파일로의 내보내기는 지원되지 않습니다.  
  
 다음 두 가지 방법으로 데이터 값을 가져올 수 있습니다.  
  
-   새 도메인을 만들고 Excel 파일에서 이 도메인으로 값을 가져옵니다. 이 경우 모든 값이 도메인에 추가됩니다.  
  
-   기존의 채워진 도메인으로 값을 가져옵니다. 이 경우 새 값만 가져옵니다. 기존의 값은 전혀 가져오지 않습니다.  
  
##  <a name="BeforeYouBegin"></a> 시작하기 전에  
  
###  <a name="Prerequisites"></a> 사전 요구 사항  
 Excel 파일에서 도메인을 가져오려면 도메인 값이나 전체 도메인을 가져오기 위해 [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)] 응용 프로그램이 설치된 컴퓨터에 Excel이 설치되어 있어야 합니다. 도메인 값이 포함된 Excel 파일을 만들어 놓은 상태여야 합니다( [How the import works](#How)참조). 그리고 도메인을 가져올 기술 자료를 만들고 열어 두어야 합니다.  
  
###  <a name="Security"></a> 보안  
  
####  <a name="Permissions"></a> Permissions  
 Excel 파일에서 도메인 값을 가져오려면 DQS_MAIN 데이터베이스의 dqs_kb_editor 또는 dqs_administrator 역할이 있어야 합니다.  
  
##  <a name="Import"></a> Import values from an Excel file into a domain  
  
1.  [!INCLUDE[ssDQSInitialStep](../includes/ssdqsinitialstep-md.md)] [Data Quality Client 응용 프로그램을 실행합니다](../data-quality-services/run-the-data-quality-client-application.md).  
  
2.  [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)] 홈 화면의 도메인 관리 작업에서 기술 자료를 엽니다.  
  
3.  새 도메인에 값을 추가하는 경우 **도메인 만들기** 아이콘을 사용하여 새 도메인을 만들고 도메인 목록에서 새 도메인을 선택합니다.  
  
4.  기존 도메인에 값을 추가하는 경우 도메인 목록에서 도메인을 선택합니다.  
  
5.  **도메인 값** 탭을 클릭하고 아이콘 표시줄에서 **값 가져오기** 아이콘을 클릭한 후 **Excel에서 유효한 값 가져오기**를 클릭합니다.  
  
6.  **도메인 값 가져오기** 대화 상자에서 **찾아보기**를 클릭합니다.  
  
7.  **파일 선택** 대화 상자에서 도메인 값을 가져올 Excel 파일이 포함된 폴더로 이동하고 파일(확장명이 .xlsx, .xls 또는 .csv)을 선택한 후 **열기**를 클릭합니다. 파일은 DQS를 실행하는 클라이언트에 있거나 사용자가 액세스할 수 있는 공유 파일에 있어야 합니다.  
  
8.  **워크시트** 드롭다운 목록에서 가져올 워크시트를 선택합니다.  
  
9. 스프레드시트의 첫 번째 행이 도메인 이름을 나타내고 나머지 모든 행이 유효한 도메인 값을 나타낼 경우 **첫 번째 행을 헤더로 사용하세요.** 를 선택합니다.  
  
10. **확인**을 클릭합니다. 성공적으로 가져온 값의 수, 가져오지 않은 값의 수 및 전체 값 수를 나타내는 진행률 표시줄이 표시됩니다. 프로세스를 취소하려면 **취소** 단추를 클릭합니다.  
  
11. "가져오기 완료"가 **도메인 값 가져오기** 대화 상자에 표시되는지 확인합니다. 이 대화 상자에서 성공적으로 가져온 값과 가져오지 않은 값을 확인합니다. 파일 이름과 파일 경로, 작업 완료 상태, 성공적으로 가져온 값의 수, 가져오지 않은 값의 수 및 처리된 전체 값의 수를 나타냅니다.  
  
12. 성공적으로 가져오지 않은 값에 대해서는 **로그** 를 클릭하여 **도메인 값 - 실패 값 가져오기** 대화 상자를 표시해 가져오기 작업이 실패한 이유를 확인합니다. **실패 값** 열에는 Excel 파일에서 도메인으로 가져오지 못한 값이 표시되고 **이유** 열은 가져오지 못한 이유를 설명합니다. **클립보드로 복사** 를 클릭하여 **실패 값** 테이블을 클립보드로 복사합니다. 여기서 Excel 스프레드시트나 메모장 파일 등의 다른 프로그램으로 테이블을 복사할 수 있습니다. **확인** 을 클릭하여 **실패 값** 대화 상자를 닫습니다.  
  
13. **확인** 을 클릭하여 가져오기 작업을 완료하고 대화 상자를 닫습니다. 가져오기가 성공적으로 완료되면 **도메인 값** 페이지의 도메인 값 목록이 새로 고쳐지고 새로 가져온 값을 포함합니다. 필터가 **모든 값** 으로 변경되고 **새 항목만 표시** 가 선택됩니다. 가져오기 작업 후 **새 항목만 표시** 가 선택되면 Excel 파일에서 가져온 값만 표시됩니다.  
  
14. **마침** 을 클릭하여 기술 자료에 값을 추가합니다.  
  
##  <a name="FollowUp"></a> 후속 작업: Excel 파일에서 도메인으로 값을 가져온 후  
 값을 도메인으로 가져온 후 도메인에 대해 다른 도메인 관리 태스크를 수행하거나, 기술 자료 검색을 수행하여 도메인에 지식을 추가하거나, 도메인에 일치 정책을 추가할 수 있습니다. 자세한 내용은 [기술 자료 검색 수행](../data-quality-services/perform-knowledge-discovery.md), [도메인 관리](../data-quality-services/managing-a-domain.md) 또는 [일치 정책 만들기](../data-quality-services/create-a-matching-policy.md)를 참조하세요.  
  
##  <a name="Synonyms"></a> 동의어 가져오기  
 동의어를 다음과 같이 가져올 수 있습니다.  
  
-   첫째, 모든 값을 가져온 후 동의어 연결이 설정됩니다.  
  
-   동의어 값을 연결할 수 없는 경우 로그 화면에 오류가 나타납니다. 파일의 선행 값과 동의어를 도메인으로 가져올 수는 있지만 동의어로 설정할 수는 없습니다.  
  
 동의어 연결 설정 프로세스에 다음이 적용됩니다.  
  
-   Excel 파일의 선행 값이 다른 값의 동의어로 이미 도메인에 있을 경우 동의어를 수동으로 설정해야 합니다. 예를 들어 Excel 파일에서 값 A가 값 B의 선행 값이지만 도메인에서는 값 A가 값 C의 동의어로 나타나도록 설정합니다. 가져오기가 완료된 후 수동으로 동의어를 설정할 뿐 아니라, 현재 동의어에 포함된 값의 연결을 해제할 수도 있습니다. 예를 들어 위의 값 A와 C의 연결을 해제합니다. 그런 다음 파일을 가져옵니다.  
  
-   동의어가 이미 다른 선행 값에 연결된 경우 동의어를 수동으로 설정해야 합니다.  
  
-   어떤 이유로든 응용 프로그램에서 수동으로 값을 연결할 수 없으면 값이 가져오기 작업에 적용되지 않습니다.  
  
##  <a name="How"></a> How the import works  
 이 작업에서 다음 값을 가져옵니다.  
  
 가져오기 작업에서 DQS는 Excel 파일을 다음과 같이 가져옵니다.  
  
-   올바른 값과 새 값을 가져옵니다. 가져온 도메인 값 중 하나 이상이 이미 있을 경우 해당 값을 가져오지 않습니다.  
  
-   도메인 규칙에 맞지 않는 값을 잘못된 값으로 가져옵니다.  
  
-   값이 도메인의 데이터 형식이 아니거나 null일 경우 값을 가져오지 않습니다.  
  
-   파일에 나타나는 순서대로 값을 가져옵니다.  
  
-   각 행은 도메인 값을 나타냅니다.  
  
-   첫 번째 행은 **첫 번째 행을 헤더로 사용하세요** 확인란의 설정에 따라 도메인 이름을 나타내거나 첫 번째 데이터 값 또는 레코드입니다. .xslx 파일이나 .xls 파일을 사용할 때 **첫 번째 행을 헤더로 사용하세요.** 를 선택할 경우 null인 열 이름은 F*n*으로 자동 변환되며 중복되는 열에는 번호가 추가됩니다.  
  
-   완료 전에 가져오기 작업을 취소하면 작업이 롤백되고 데이터를 가져오지 않습니다.  
  
-   첫 번째 열의 값을 도메인으로 가져옵니다. 첫 번째 열 외에 하나 이상의 추가 열이 채워지면 해당 열의 값이 동의어로 추가됩니다. [동의어 가져오기](#Synonyms)를 참조하세요.  
  
    -   첫 번째 열이 선행 열이 되고 두 번째 열부터 동의어가 되어야 합니다.  
  
    -   같은 행이나 다른 행에서 여러 동의어를 가져올 수 있습니다. 예를 들어 “NYC”와 “New York City”를 “New York”의 동의어로 가져오려는 경우 열 1에 “New York”이 있고 열 2에 “NYC”가 있고 열 3에 “New York City”가 있는 단일 행을 가져오거나, 열 1에 “New York”이 있고 열 2에 “NYC”가 있는 행 한 개와 열 1에 “New York”이 있고 열 2에 “New York City”가 있는 또 다른 행을 가져올 수 있습니다. 값 “New York”이 이미 도메인에 있으면 동의어만 추가되며, 가져오기 프로세스 도중에 값이 이미 있다는 내용의 오류가 사용자에게 표시되지 않습니다. 첫 번째 값이 아직 없으면 도메인에 추가됩니다.  
  
 가져오기에 사용되는 Excel 파일에 다음 규칙이 적용됩니다.  
  
-   Excel 파일의 확장명은 .xlsx, .xls 또는 .csv입니다. 도메인 값 또는 전체 도메인을 가져오려면 [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)] 응용 프로그램이 설치된 컴퓨터에 Microsoft Excel이 설치되어 있어야 합니다. Excel 2003 이상 버전이 지원됩니다. 64비트 버전의 Excel이 사용된 경우 Excel 2003 파일만 지원됩니다. Excel 2007 또는 2010 파일은 지원되지 않습니다.  
  
-   Excel 파일 형식 .xlsx는 Excel 64비트 설치에서 지원되지 않습니다. 64비트 Excel을 사용하는 경우 스프레드시트 파일을 .xls 파일 또는 .csv 파일로 저장하거나 Excel 32비트 설치를 대신 설치하세요.  
  
-   .xlsx 및 .xls 파일에서는 처음 8개 행에 따라 열의 데이터 형식이 결정됩니다. 처음 8개 행의 열 데이터 형식이 혼합된 경우 열 형식은 문자열입니다. 행 9 이상의 셀이 데이터 형식을 따르지 않을 경우 null 값이 지정됩니다.  
  
-   .csv 파일에서는 처음 8개 행에서 가장 많이 사용된 데이터 형식에 의해 데이터 형식이 결정됩니다.  
  
-   Excel 파일이 올바른 형식이 아니거나 손상된 경우 가져오기 작업에서 오류가 발생합니다.  
  
  
