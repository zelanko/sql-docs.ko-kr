---
title: CLR 데이터베이스 개체 배포 | Microsoft Docs
description: Microsoft Visual Studio를 사용 하 여 SQL Server에 대 한 CLR 데이터베이스 개체를 개발 하 고 테스트 서버에 배포 하 여 프로덕션 서버에 배포할 수 있습니다.
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: clr
ms.topic: reference
helpviewer_keywords:
- deployment script [CLR integration]
- common language runtime [SQL Server], deploying
- deploying assemblies [CLR integration]
- deploying [CLR integration]
ms.assetid: 00752573-3367-41a7-af98-7b7a29e8e2f2
author: rothja
ms.author: jroth
ms.openlocfilehash: 88f297829a13c1b7d132230aebab76b9f546704d
ms.sourcegitcommit: cfa04a73b26312bf18d8f6296891679166e2754d
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/19/2020
ms.locfileid: "92192613"
---
# <a name="deploying-clr-database-objects"></a>CLR 데이터베이스 개체 배포
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  배포는 완성된 애플리케이션이나 모듈을 배포하여 다른 컴퓨터에서 설치하고 실행하는 프로세스입니다. [!INCLUDE[msCoName](../../includes/msconame-md.md)] Visual Studio를 사용하면 CLR(공용 언어 런타임) 데이터베이스 개체를 개발하고 테스트 서버에 배포할 수 있습니다. 또는 Visual Studio 대신 [!INCLUDE[msCoName](../../includes/msconame-md.md)] .NET Framework 재배포 파일을 사용하여 관리되는 데이터베이스 개체를 컴파일할 수도 있습니다. 컴파일되고 나면 CLR 데이터베이스 개체가 포함된 어셈블리를 Visual Studio 또는 [!INCLUDE[tsql](../../includes/tsql-md.md)] 문을 사용하여 테스트 서버에 배포할 수 있습니다. Visual Studio .NET 2003은 CLR 통합 프로그래밍이나 배포에 사용할 수 없습니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에는 .NET Framework가 미리 설치되어 있으며 Visual Studio .NET 2003에서는 .NET Framework 2.0 어셈블리를 사용할 수 없습니다.  
  
 테스트 서버에서 CLR 메서드를 테스트하고 확인하고 나면 개발 스크립트를 사용하여 프로덕션 서버에 배포할 수 있습니다. 개발 스크립트는 수동으로 생성하거나 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]를 사용하여 생성할 수 있습니다. 자세한 내용은 이 항목의 뒷부분에 나오는 절차를 참조하십시오.  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서는 CLR 통합 기능이 기본적으로 해제되어 있으므로 CLR 어셈블리를 사용하려면 이 기능을 사용하도록 설정해야 합니다. 자세한 내용은 [Enabling CLR Integration](../../relational-databases/clr-integration/clr-integration-enabling.md)을 참조하세요.  
  
## <a name="deploying-the-assembly-to-the-test-server"></a>테스트 서버에 어셈블리 배포  
 Visual Studio를 사용하여 CRL 함수, 프로시저, 트리거, UDT(사용자 정의 형식), UDA(사용자 정의 집계)를 만들고 테스트 서버에 배포할 수 있습니다. 또한 .NET Framework 재배포 파일에 포함된 csc.exe 및 vbc.exe와 같은 명령줄 컴파일러를 사용하여 이러한 관리되는 데이터베이스 개체를 컴파일할 수도 있습니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]용 관리되는 데이터베이스 개체를 개발하기 위해 Visual Studio 통합 개발 환경이 필요한 것은 아닙니다.  
  
 모든 컴파일러 오류와 경고를 해결해야 합니다. 그런 다음 Visual Studio나 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 문을 사용하여 CLR 루틴이 포함된 어셈블리를 [!INCLUDE[tsql](../../includes/tsql-md.md)] 데이터베이스에 등록할 수 있습니다.  
  
> [!NOTE]  
>  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Visual Studio를 원격 개발, 디버깅 및 개발에 사용하려면 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 인스턴스에서 TCP/IP 네트워크 프로토콜을 사용할 수 있어야 합니다. 서버에서 TCP/IP 프로토콜을 사용 하도록 설정 하는 방법에 대 한 자세한 내용은 [클라이언트 프로토콜 구성](../../database-engine/configure-windows/configure-client-protocols.md)을 참조 하세요.  
  
#### <a name="to-deploy-the-assembly-using-visual-studio"></a>Visual Studio를 사용하여 어셈블리를 배포하려면  
  
1.  **Build** \<project name> **빌드** 메뉴에서 빌드를 선택 하 여 프로젝트를 빌드합니다.  
  
2.  테스트 서버에 어셈블리를 배포하기 전에 모든 빌드 오류 및 경고를 해결합니다.  
  
3.  **빌드** 메뉴에서 **배포** 를 선택 합니다. 그러면 Visual Studio에서 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 프로젝트를 처음 만들 때 지정한 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스와 데이터베이스에 어셈블리가 등록됩니다.  

#### <a name="to-deploy-the-assembly-using-transact-sql"></a>Transact-SQL을 사용하여 어셈블리를 배포하려면  
  
1.  .NET Framework에 포함된 명령줄 컴파일러를 사용하여 원본 파일에서 어셈블리를 컴파일합니다.  
  
2.  [!INCLUDE[msCoName](../../includes/msconame-md.md)] Visual C# 원본 파일의 경우 다음 명령을 실행합니다.  
  
3.  `csc /target:library C:\helloworld.cs`  
  
4.  [!INCLUDE[msCoName](../../includes/msconame-md.md)] Visual Basic 원본 파일의 경우 다음 명령을 실행합니다.  
  
 `vbc /target:library C:\helloworld.vb`  
  
 이러한 명령은 **/target** 옵션을 사용 하 여 Visual c # 또는 Visual Basic 컴파일러를 시작 하 여 라이브러리 DLL 빌드를 지정 합니다.  
  
1.  테스트 서버에 어셈블리를 배포하기 전에 모든 빌드 오류 및 경고를 해결합니다.  
  
2.  테스트 서버에서 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]를 엽니다. AdventureWorks와 같은 적절한 테스트 서버에 연결된 새 쿼리를 만듭니다.  
  
3.  쿼리에 다음 [!INCLUDE[tsql](../../includes/tsql-md.md)]을 추가하여 서버에서 어셈블리를 만듭니다.  
  
 `CREATE ASSEMBLY HelloWorld from 'c:\helloworld.dll' WITH PERMISSION_SET = SAFE;`  
  
1.  그런 다음 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]의 인스턴스에서 프로시저, 함수, 집계, 사용자 정의 형식 또는 트리거를 만들어야 합니다. **Helloworld** 어셈블리에 procedure **클래스의** **helloworld** 라는 메서드가 포함 된 경우에는 다음을 [!INCLUDE[tsql](../../includes/tsql-md.md)] 쿼리에 추가 하 여 **hello** 라는 프로시저를 만들 수 있습니다 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
 `CREATE PROCEDURE hello`  
  
 `AS`  
  
 `EXTERNAL NAME HelloWorld.Procedures.HelloWorld`  
  
 에서 다양 한 유형의 관리 되는 데이터베이스 개체를 만드는 방법에 대 한 자세한 내용은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [Clr User-Defined 함수](../../relational-databases/clr-integration-database-objects-user-defined-functions/clr-user-defined-functions.md), [clr User-Defined 집계](../../relational-databases/clr-integration-database-objects-user-defined-functions/clr-user-defined-aggregates.md), Clr [User-Defined 유형](../../relational-databases/clr-integration-database-objects-user-defined-types/clr-user-defined-types.md), clr [저장 프로시저](/dotnet/framework/data/adonet/sql/clr-stored-procedures)및 [clr 트리거](/dotnet/framework/data/adonet/sql/clr-triggers)를 참조 하세요.  
  
## <a name="deploying-the-assembly-to-production-servers"></a>프로덕션 서버에 어셈블리 배포  
 테스트 서버에서 CLR 데이터베이스 개체를 테스트하고 확인하고 나면 프로덕션 서버에 배포할 수 있습니다. 관리 되는 데이터베이스 개체를 디버깅 하는 방법에 대 한 자세한 내용은 [CLR 데이터베이스 개체 디버깅](../../relational-databases/clr-integration/debugging-clr-database-objects.md)을 참조 하십시오.  
  
 관리되는 데이터베이스 개체의 배포는 테이블, [!INCLUDE[tsql](../../includes/tsql-md.md)] 루틴 등과 같은 일반 데이터베이스 개체의 배포와 유사합니다. 즉, CLR 데이터베이스 개체가 포함된 어셈블리를 배포 스크립트를 사용하여 다른 서버에 배포할 수 있습니다. 배포 스크립트는 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]의 "스크립트 생성" 기능을 사용하여 작성할 수 있습니다. 또한 배포 스크립트는 수동으로 작성하거나 "스크립트 생성"을 사용하여 작성할 수 있고 수동으로 변경할 수도 있습니다. 배포 스크립트를 작성하고 나면 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]의 다른 인스턴스에서 실행하여 관리되는 데이터베이스 개체를 배포할 수 있습니다.  
  
#### <a name="to-generate-a-deployment-script-using-generate-scripts"></a>스크립트 생성을 사용하여 배포 스크립트를 생성하려면  
  
1.  [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]를 열고 배포할 관리되는 어셈블리나 데이터베이스 개체가 등록된 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스에 연결합니다.  
  
2.  **개체 탐색기**에서 **\<server name>** 및 **데이터베이스** 트리를 확장 합니다. 관리 되는 데이터베이스 개체가 등록 된 데이터베이스를 마우스 오른쪽 단추로 클릭 하 고 **태스크**를 선택한 다음 **스크립트 생성**을 선택 합니다. 스크립트 마법사가 열립니다.  
  
3.  목록 상자에서 데이터베이스를 선택 하 고 **다음**을 클릭 합니다.  
  
4.  **스크립트 옵션 선택** 창에서 **다음**을 클릭 하거나 옵션을 변경한 후 **다음**을 클릭 합니다.  
  
5.  **개체 유형 선택** 창에서 배포할 데이터베이스 개체의 유형을 선택 합니다. **다음**을 클릭합니다.  
  
6.  **개체 형식 선택** 창에서 선택한 모든 개체 형식에 대해 ** \<type> 선택** 창이 표시 됩니다. 이 창에서 지정된 데이터베이스에 등록된 해당 데이터베이스 개체 유형의 모든 인스턴스 중에서 선택할 수 있습니다. 하나 이상의 개체를 선택 하 고 **다음**을 클릭 합니다.  
  
7.  원하는 모든 데이터베이스 개체 유형을 선택 하면 **출력 옵션** 창이 나타납니다. **파일에 스크립트를** 선택 하 고 스크립트의 파일 경로를 지정 합니다. **다음**을 선택합니다. 선택 항목을 검토 하 고 **마침**을 클릭 합니다. 배포 스크립트가 저장된 파일 경로에 저장됩니다.  
  
## <a name="post-deployment-scripts"></a>배포 후 스크립트  
 배포 후 스크립트를 실행할 수 있습니다.  
  
 배포 후 스크립트를 추가하려면 Visual Studio 프로젝트 디렉터리에 postdeployscript.sql이라는 파일을 추가합니다. 예를 들어 **솔루션 탐색기** 에서 프로젝트를 마우스 오른쪽 단추로 클릭 하 고 **기존 항목 추가**를 선택 합니다. 테스트 스크립트 폴더가 아닌 프로젝트의 루트에 있는 파일을 추가합니다.  
  
 배포를 클릭하면 Visual Studio에서 프로젝트 배포 후에 이 스크립트를 실행합니다.  
  
## <a name="see-also"></a>참고 항목  
 [CLR&#40;공용 언어 런타임&#41; 통합 프로그래밍 개요](../../relational-databases/clr-integration/common-language-runtime-clr-integration-programming-concepts.md)  
  
