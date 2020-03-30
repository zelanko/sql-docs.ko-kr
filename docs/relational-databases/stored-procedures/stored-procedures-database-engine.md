---
title: 저장 프로시저(데이터베이스 엔진) | Microsoft 문서
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.technology: stored-procedures
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- storing programs as stored procedures
- stored procedures [SQL Server], about stored procedures
ms.assetid: cc6daf62-9663-4c3e-950a-ab42e2830427
author: stevestein
ms.author: sstein
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: e64a097fb4d2eed917155fb3881d233231c413bc
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/30/2020
ms.locfileid: "70148302"
---
# <a name="stored-procedures-database-engine"></a>저장 프로시저(데이터베이스 엔진)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]의 저장 프로시저는 하나 이상의 [!INCLUDE[tsql](../../includes/tsql-md.md)] 문 그룹이거나 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] CLR(공용 언어 런타임) 메서드에 대한 참조입니다. 프로시저는 다음과 같은 점에서 다른 프로그래밍 언어의 구문과 유사합니다.  
  
-   입력 매개 변수를 받아 여러 값을 출력 매개 변수의 형태로 호출하는 프로그램에 반환합니다.  
  
-   데이터베이스에서 작업을 수행하는 프로그래밍 문을 포함합니다. 여기에는 호출하는 다른 프로시저가 포함됩니다.  
  
-   호출하는 프로그램에 상태 값을 반환하여 성공 또는 실패 및 실패 원인을 나타냅니다.  
  
## <a name="benefits-of-using-stored-procedures"></a>저장 프로시저를 사용할 경우의 이점  
 다음 목록에서는 프로시저를 사용할 경우의 몇 가지 이점에 대해 설명합니다.  
  
 서버/클라이언트 네트워크 트래픽 감소  
 프로시저의 명령은 단일 일괄 처리 코드로 실행됩니다. 따라서 프로시저를 실행할 호출만 네트워크에서 전송되기 때문에 서버와 클라이언트 간의 네트워크 트래픽이 크게 줄어들 수 있습니다. 프로시저에서 제공하는 코드 캡슐화가 없으면 모든 개별 코드 줄이 네트워크를 교차해야 합니다.  
  
 보안 강화  
 여러 사용자 및 클라이언트 프로그램이 기본 데이터베이스 개체에 대한 직접적인 사용 권한이 없는 경우에도 프로시저를 통해 이러한 기본 개체에 대해 작업을 수행할 수 있습니다. 프로시저는 수행되는 프로세스 및 작업을 제어하고 기본 데이터베이스 개체를 보호합니다. 따라서 개별 개체 수준에서 사용 권한을 부여할 필요가 없으며 보안 계층이 간소화됩니다.  
  
 [EXECUTE AS](../../t-sql/statements/execute-as-clause-transact-sql.md) 절을 CREATE PROCEDURE 문에 지정하여 다른 사용자를 가장하거나 사용자 또는 애플리케이션에서 기본 개체 및 명령에 대한 직접적인 사용 권한 없이도 특정 데이터베이스 작업을 수행할 수 있도록 할 수 있습니다. 예를 들어 TRUNCATE TABLE 등의 일부 동작에는 부여할 수 있는 권한이 없습니다. TRUNCATE TABLE을 실행하려면 사용자가 지정된 테이블에 대한 ALTER 권한을 가지고 있어야 합니다. 사용자가 너무 큰 권한을 갖게 되어 테이블을 자를 수도 있으므로 사용자에게 테이블에 대한 ALTER 권한을 부여하는 것은 최상의 방법이 아닙니다. TRUNCATE TABLE 문을 모듈에 통합하고 테이블 수정 권한을 가진 사용자로 모듈이 실행되도록 지정하면 테이블 자르기 권한을 모듈에 대해 EXECUTE 권한을 부여한 사용자에게로 확장할 수 있습니다.  
  
 네트워크를 통해 프로시저를 호출하면 프로시저를 실행할 호출만 표시됩니다. 따라서 악의적인 사용자가 테이블 및 데이터베이스 개체 이름을 보거나 [!INCLUDE[tsql](../../includes/tsql-md.md)] 문을 포함하거나 중요한 데이터를 검색할 수 없습니다.  
  
 프로시저 매개 변수를 사용하면 SQL 삽입 공격으로부터 보호하는 데 도움이 됩니다. 매개 변수 입력은 실행 코드가 아니라 리터럴 값으로 처리되므로 공격자가 프로시저 내의 [!INCLUDE[tsql](../../includes/tsql-md.md)] 문에 명령을 삽입하여 보안을 손상시키기가 보다 어렵습니다.  
  
 프로시저를 암호화하여 원본 코드를 난독 처리할 수 있습니다. 자세한 내용은 [SQL Server Encryption](../../relational-databases/security/encryption/sql-server-encryption.md)를 참조하세요.  
  
 코드 재사용  
 반복적인 모든 데이터베이스 작업의 코드는 프로시저에서 캡슐화하기에 가장 완벽한 대상입니다. 이러한 코드를 캡슐화하면 같은 코드를 다시 작성할 필요가 없으며, 코드 불일치가 감소되고, 필요한 권한을 가진 사용자 또는 애플리케이션에서 코드에 액세스하여 코드를 실행할 수 있습니다.  
  
 보다 간편한 유지 관리  
 클라이언트 애플리케이션에서 프로시저를 호출하고 데이터베이스 작업을 데이터 계층에 유지하면 기본 데이터베이스의 모든 변경 내용에 대해 프로시저만 업데이트하면 됩니다. 애플리케이션 계층은 별도의 계층으로 유지되므로 데이터베이스 레이아웃, 관계 또는 프로세스에 대한 변경 내용을 알 필요가 없습니다.  
  
 성능 향상  
 기본적으로 프로시저는 처음 실행될 때 컴파일되며 이후 실행에 다시 사용되는 실행 계획을 만듭니다. 쿼리 프로세서는 새 계획을 만들 필요가 없으므로 일반적으로 프로시저 처리 시간이 줄어듭니다.  
  
 프로시저에서 참조하는 테이블이나 데이터가 크게 변경된 경우에는 미리 컴파일된 계획으로 인해 실제로 프로시저 실행 속도가 느려질 수 있습니다. 이 경우 프로시저를 다시 컴파일하고 새 실행 계획을 강제 적용하면 성능을 향상시킬 수 있습니다.  
  
## <a name="types-of-stored-procedures"></a>저장 프로시저 유형  

 **사용자 정의**  
 **Resource** 데이터베이스를 제외한 모든 시스템 데이터베이스 또는 사용자 정의 데이터베이스에서 사용자 정의 프로시저를 만들 수 있습니다. 이 프로시저는 [!INCLUDE[tsql](../../includes/tsql-md.md)] 또는 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] CLR(공용 언어 런타임) 메서드에 대한 참조로 개발될 수 있습니다.  
  
 **임시**  
 임시 프로시저는 사용자 정의 프로시저에 속합니다. 임시 프로시저는 **tempdb**에 저장된다는 점을 제외하고는 영구 프로시저와 유사합니다. 임시 프로시저에는 로컬 및 전역의 두 가지 유형이 있습니다. 이 두 유형은 이름, 표시 여부 및 가용성 면에서 서로 다릅니다. 로컬 임시 프로시저는 이름이 하나의 숫자 기호(#)로 시작하며 현재 사용자 연결에만 표시되고 연결이 닫히면 삭제됩니다. 전역 임시 프로시저는 이름이 두 개의 숫자 기호(##)로 시작하며 생성된 후 모든 사용자에게 표시되고 해당 프로시저를 사용하는 마지막 세션이 끝나면 삭제됩니다.  
  
 **시스템**  
 시스템 프로시저는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에 포함됩니다. 이러한 프로시저는 물리적으로 **Resource** 데이터베이스에 저장되지만 논리적으로는 모든 시스템 정의 데이터베이스와 사용자 정의 데이터베이스의 **sys** 스키마에 표시됩니다. 또한 **msdb** 데이터베이스에도 **dbo** 스키마에 경고 및 작업을 예약하는 데 사용되는 시스템 저장 프로시저가 있습니다. 시스템 프로시저는 **sp_** 접두사로 시작하므로 사용자 정의 프로시저의 이름을 지정할 때 이 접두사를 사용하지 않는 것이 좋습니다. 시스템 저장 프로시저의 전체 목록은 [시스템 저장 프로시저&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)를 참조하세요.  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에서는 다양한 유지 관리 작업을 수행할 수 있도록 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 의 인터페이스를 외부 프로그램에 제공하는 시스템 프로시저를 지원합니다. 이러한 확장 프로시저에는 xp_ 접두사가 사용됩니다. 확장 저장 프로시저의 전체 목록은 [일반 확장 저장 프로시저&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/general-extended-stored-procedures-transact-sql.md)를 참조하세요.  
  
 **확장 사용자 정의**  
 확장 프로시저를 사용하면 C와 같은 프로그래밍 언어로 외부 루틴을 작성할 수 있습니다. 이러한 프로시저는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스에서 동적으로 로드 및 실행할 수 있는 DLL입니다.  
  
> [!NOTE]  
>  확장 저장 프로시저는 이후 버전의 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 제거될 예정입니다. 새 개발 작업에서는 이 기능을 사용하지 말고, 현재 이 기능을 사용하는 애플리케이션은 가능한 한 빨리 수정하세요. 대신 CLR 프로시저를 만들어야 합니다. 이 메서드를 사용하면 확장 프로시저를 보다 강력하고 안전한 방법으로 작성할 수 있습니다.  
  
## <a name="related-tasks"></a>관련 작업  
  
|||  
|-|-|  
|**태스크 설명**|**항목**|  
|저장 프로시저를 만드는 방법에 대해 설명합니다.|[저장 프로시저 만들기](../../relational-databases/stored-procedures/create-a-stored-procedure.md)|  
|저장 프로시저를 수정하는 방법에 대해 설명합니다.|[저장 프로시저 수정](../../relational-databases/stored-procedures/modify-a-stored-procedure.md)|  
|저장 프로시저를 삭제하는 방법에 대해 설명합니다.|[저장 프로시저 삭제](../../relational-databases/stored-procedures/delete-a-stored-procedure.md)|  
|저장 프로시저를 실행하는 방법에 대해 설명합니다.|[저장 프로시저 실행](../../relational-databases/stored-procedures/execute-a-stored-procedure.md)|  
|저장 프로시저에 대한 사용 권한을 부여하는 방법에 대해 설명합니다.|[저장 프로시저에 대한 사용 권한 부여](../../relational-databases/stored-procedures/grant-permissions-on-a-stored-procedure.md)|  
|저장 프로시저에서 애플리케이션에 데이터를 반환하는 방법에 대해 설명합니다.|[저장 프로시저에서 데이터 반환](../../relational-databases/stored-procedures/return-data-from-a-stored-procedure.md)|  
|저장 프로시저를 다시 컴파일하는 방법에 대해 설명합니다.|[저장 프로시저 다시 컴파일](../../relational-databases/stored-procedures/recompile-a-stored-procedure.md)|  
|저장 프로시저의 이름을 바꾸는 방법에 대해 설명합니다.|[저장 프로시저 이름 바꾸기](../../relational-databases/stored-procedures/rename-a-stored-procedure.md)|  
|저장 프로시저의 정의를 보는 방법에 대해 설명합니다.|[저장 프로시저의 정의 보기](../../relational-databases/stored-procedures/view-the-definition-of-a-stored-procedure.md)|  
|저장 프로시저의 종속성을 보는 방법에 대해 설명합니다.|[저장 프로시저의 종속성 보기](../../relational-databases/stored-procedures/view-the-dependencies-of-a-stored-procedure.md)|  
|저장 프로시저에서 매개 변수를 사용하는 방법을 설명합니다.|[매개 변수](../../relational-databases/stored-procedures/parameters.md)|  
  
## <a name="related-content"></a>관련 내용  
 [CLR 저장 프로시저](https://docs.microsoft.com/dotnet/framework/data/adonet/sql/clr-stored-procedures)  
 [지연된 이름 확인](../../t-sql/statements/create-trigger-transact-sql.md#deferred-name-resolution)
  
