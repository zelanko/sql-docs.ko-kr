---
title: "SQL Server (DB2ToSQL)에 연결 | Microsoft Docs"
ms.prod: sql-non-specified
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: 
ms.technology: sql-ssma
ms.tgt_pltfrm: 
ms.topic: article
applies_to:
- Azure SQL Database
- SQL Server
ms.assetid: bc14a072-8949-4ee0-a4b4-ada55fe8df5c
caps.latest.revision: "3"
author: Shamikg
ms.author: Shamikg
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 1d242bd56757ce32dedaab7287ac3c1ad64b9a08
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/09/2017
---
# <a name="connect-to-sql-server-db2tosql"></a>SQL Server (DB2ToSQL)에 연결
사용 하 여 **SQL Server에 연결** 의 인스턴스에 연결 하는 대화 상자 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 로 마이그레이션하려는 합니다. 에 액세스 하려면는 **SQL Server에 연결** 대화 상자의 **파일** 메뉴를 클릭 하 여 **SQL Server에 연결**합니다.  
  
## <a name="options"></a>옵션  
**서버 이름**  
입력 하거나 연결할 SQL Server의 인스턴스를 선택 합니다. 기본적으로 가장 최근에에 연결 하는 인스턴스로 표시 됩니다.  
  
-   로컬 컴퓨터의 기본 인스턴스에 연결 하는 경우 하나를 입력 **localhost** 또는 점 (**.**).  
  
-   다른 컴퓨터의 기본 인스턴스에 연결 하는 경우에 컴퓨터의 이름을 입력 합니다.  
  
-   다른 컴퓨터에 명명 된 인스턴스에 연결 하는 경우 컴퓨터 이름, 백슬래시 및 인스턴스 이름을 같은 입력 *MyServer*\\*MyInstance*합니다.  
  
**서버 포트**  
경우 인스턴스의 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 기본 연결 포트 (1433), 포트 번호를 입력을 허용 하도록 구성 되지 않았습니다. 그렇지 않은 경우이 값 비워 둡니다.  
  
**데이터베이스**  
개체와 데이터를 마이그레이션할 데이터베이스를 지정 합니다. 다시 연결할 때이 옵션을 사용할 수 없습니다 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]합니다.  
  
**인증**  
에 연결 하는 데 사용 되는 인증 방법을 선택 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]합니다. 현재 Windows 계정을 사용 하려면 Windows 인증을 선택 합니다. 지정 하는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 로그인과 암호를 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 인증 합니다.  
  
**사용자 이름**  
사용 중인 경우 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 인증의 경우 해당 인스턴스에 대 한 로그인을 입력 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]합니다. Windows 인증을 사용 하는 경우이 옵션은 사용할 수 없습니다.  
  
**암호**  
사용 중인 경우 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 인증을 해당 인스턴스의 로그인에 대 한 암호를 입력 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]합니다. Windows 인증을 사용 하는 경우이 옵션은 사용할 수 없습니다.  
  
**연결 암호화**  
SQL Server에 안전 하 게 연결 하려는 경우 선택 하 여 사용할 연결 암호화의는 **연결 암호화** 확인란을 선택 합니다.  
  
**서버 인증서 신뢰**  
이 옵션을 사용 하려는 경우 선택 된 **서버 인증서 신뢰** 확인란을 선택 합니다.  
  
> [!NOTE]  
> 사용할 수 있도록 **서버 인증서 신뢰**, "암호화"로 설정 해야 **True**합니다.  
  
