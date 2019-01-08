---
title: SQL Server (AccessToSQL)에 연결 | Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: ceb77a97-d6d5-4a92-90a6-342e97d12b54
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.openlocfilehash: 7a3e6b18377f01d93dfb4bdda840bc6abc0dafee
ms.sourcegitcommit: 1ab115a906117966c07d89cc2becb1bf690e8c78
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/27/2018
ms.locfileid: "52414480"
---
# <a name="connect-to-sql-server-accesstosql"></a>SQL Server (AccessToSQL)에 연결
사용 된 **SQL Server에 연결** 의 인스턴스에 연결 하려면 대화 상자 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 를 마이그레이션하려는 합니다. 액세스는 **SQL Server에 연결** 대화 상자의 합니다 **파일** 메뉴에서 클릭 **SQL Server에 연결**합니다.  
  
## <a name="options"></a>변수  
**서버 이름**  
입력 하거나 연결할 SQL Server 인스턴스를 선택 합니다. 기본적으로 가장 최근에 연결 된 인스턴스가 표시 됩니다.  
  
-   로컬 컴퓨터의 기본 인스턴스에 연결 하는 경우 중 하나를 입력할 수 있습니다 **localhost** 또는 점 (**.**).  
  
-   다른 컴퓨터의 기본 인스턴스에 연결 하는 경우에 컴퓨터의 이름을 입력 합니다.  
  
-   다른 컴퓨터에 명명 된 인스턴스에 연결 하는 경우 컴퓨터 이름, 백슬래시 및 인스턴스 이름을 같은 입력 *MyServer*\\*MyInstance*합니다.  
  
**서버 포트**  
경우 인스턴스의 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 기본 연결 포트 (1433), 포트 번호를 입력을 수락 하도록 구성 되지 않았습니다. 그렇지 않은 경우이 값 비워 둡니다.  
  
**데이터베이스 백업**  
개체와 데이터를 마이그레이션할 데이터베이스를 지정 합니다. 다시 연결할 때이 옵션을 사용할 수 없습니다 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]합니다.  
  
**인증**  
연결에 사용 되는 인증 방법을 선택 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]합니다. 에서 현재 Windows 계정을 사용 하려면 Windows 인증을 선택 합니다. 지정 된 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 로그인 및 암호를 선택 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인증 합니다.  
  
**사용자 이름**  
사용 중인 경우 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인증 로그인의 해당 인스턴스에 대 한 입력 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]합니다. Windows 인증을 사용 하는 경우이 옵션이 제공 되지 않습니다.  
  
**암호**  
사용 중인 경우 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인증을 해당 인스턴스의 로그인에 대 한 암호를 입력 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]합니다. Windows 인증을 사용 하는 경우이 옵션이 제공 되지 않습니다.  
  
**연결 암호화**  
SQL Server에 안전 하 게 연결 하려는 경우 확인 하 여 암호화 연결 사용 합니다 **연결 암호화** 확인란을 선택 합니다.  
  
**서버 인증서 신뢰**  
이 옵션을 사용 하려는 경우 선택 합니다 **서버 인증서 신뢰** 확인란을 선택 합니다.  
  
> [!NOTE]  
> 사용할 수 있도록 **서버 인증서 신뢰**, "암호화"로 설정 해야 **True**합니다.  
  
