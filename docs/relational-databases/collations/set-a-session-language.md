---
title: 세션 언어 설정 | Microsoft 문서
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- errors [SQL Server], international considerations
- globalization [SQL Server], sessions
- time [SQL Server]
- sessions [SQL Server], languages
- international considerations [SQL Server], sessions
- dates [SQL Server], session languages
- global considerations [SQL Server], sessions
- client-side session language
- time [SQL Server], session languages
- messages [SQL Server], international considerations
- server-side session language
ms.assetid: de7f2c90-8f4f-4cfc-94cc-4933a7fd2bde
author: stevestein
ms.author: sstein
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 201dbacf7ce2dde7cb3da387bbfd79070e1790ed
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68140874"
---
# <a name="set-a-session-language"></a>세션 언어 설정
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  세션 언어를 사용하여 언어 및 문화 기본 설정을 기반으로 다음과 같은 요소가 서버에 표시되는 방식을 설정할 수 있습니다.  
  
-   오류 및 기타 시스템 메시지에 사용될 언어입니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에서는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 가 지역화된 모든 언어로 모든 시스템 오류 문자열 및 메시지의 복사본을 여러 개 만들 수 있습니다. 이러한 메시지는 [sys.messages](../../relational-databases/system-catalog-views/messages-for-errors-catalog-views-sys-messages.md) 카탈로그 뷰를 사용하여 볼 수 있습니다. 해당 언어 버전의 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]를 설치하면 이러한 시스템 메시지가 해당 언어로 변환됩니다. 기본적으로 이러한 메시지의 영어(미국) 집합이 포함됩니다. 또한 [sp_addmessage](../../relational-databases/system-stored-procedures/sp-addmessage-transact-sql.md)를 사용하여 특정 언어의 사용자 정의 메시지를 추가할 수 있습니다.  
  
-   날짜 및 시간 데이터의 형식  
  
-   요일 및 월 이름(약어 포함)  
  
-   시작 요일  
  
-   통화 데이터  
  
 33가지의 서로 다른 언어를 세션 설정으로 사용할 수 있습니다. 언어 목록을 보려면 [sys.syslanguages](../../relational-databases/system-compatibility-views/sys-syslanguages-transact-sql.md)를 참조하십시오.  
  
## <a name="setting-the-session-language-from-the-server"></a>서버에서 세션 언어 설정  
 서버 쪽에서 세션 언어를 설정하려면 [SET LANGUAGE](../../t-sql/statements/set-language-transact-sql.md)를 사용합니다.  
  
## <a name="setting-the-session-language-from-the-client"></a>클라이언트에서 세션 언어 설정  
 OLE DB, ODBC 또는 ADO.NET을 사용하여 클라이언트 쪽에서 세션 언어를 설정할 수 있습니다. OLE DB의 경우 SSPROP_INIT_CURRENTLANGUAGE 속성을 사용합니다. 자세한 내용은 [초기화 및 권한 부여 속성](../../relational-databases/native-client-ole-db-data-source-objects/initialization-and-authorization-properties.md)을 참조하세요.  
  
 ODBC의 경우 Language 키워드를 사용합니다. 자세한 내용은 [SQLConfigDataSource](../../relational-databases/native-client-odbc-api/sqlconfigdatasource.md)을 참조하세요.  
  
 ADO.NET의 경우 **ConnectionString** 개체의 **Current Language** 매개 변수를 사용합니다. 자세한 내용은 [!INCLUDE[msCoName](../../includes/msconame-md.md)] MDAC(데이터 액세스 구성 요소) SDK(소프트웨어 개발 키트) 설명서를 참조하십시오.  
  
  
