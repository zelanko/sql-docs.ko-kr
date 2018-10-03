---
title: 메모리 액세스에 최적화된 테이블 구독자로 복제 | Microsoft 문서
ms.custom: ''
ms.date: 03/08/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- replication
ms.topic: conceptual
ms.assetid: 1a8e6bc7-433e-471d-b646-092dc80a2d1a
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 0f1ec48661147c78449e7767e87bafd475bb7819
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48128653"
---
# <a name="replication-to-memory-optimized-table-subscribers"></a>메모리 액세스에 최적화된 테이블 구독자로 복제
  피어 투 피어 트랜잭션 복제를 제외하고 트랜잭션 복제 구독자 역할을 수행하는 테이블은 메모리 최적화 테이블로 구성할 수 있습니다. 다른 복제 구성은 메모리 최적화 테이블과 호환되지 않습니다.  
  
## <a name="configuring-a-memory-optimized-table-as-a-subscriber"></a>메모리 최적화 테이블을 구독자로 구성  
 메모리 최적화 테이블을 구독자로 구성하려면 다음 단계를 수행합니다.  
  
 **게시 만들기 및 사용**  
  
1.  게시 생성  
  
2.  아티클을 게시에 추가합니다. `@upd_cmd` 매개 변수에 대해서는 SCALL 또는 SQL 규칙을 사용합니다.  
  
    ```  
    EXEC sp_addarticle  
        @publication = N'Publication1',  
        @article = N'Mem_Table',  
        @source_owner = N'dbo',  
        @source_object = N'Mem_Table',  
        @type = N'logbased',  
        @description = null,  
        @creation_script = null,  
        @pre_creation_cmd = N'none',  
        @schema_option = 0x00000000080050DF,  
        @identityrangemanagementoption = N'manual',  
        @destination_table = N'Mem_Table',  
        @destination_owner = N'dbo',  
        @vertical_partition = N'false',  
        @ins_cmd = N'CALL sp_MSins_Mem_Table',  
        @del_cmd = N'CALL sp_MSdel_Mem_Table',  
        @upd_cmd = N'SCALL sp_MSupd_Mem_Table';  
    GO  
    ```  
  
 **스냅숏을 생성 하 고 스키마 조정**  
  
1.  스냅숏 작업을 만들고 스냅숏을 생성합니다.  
  
    ```  
    EXEC sp_addpublication_snapshot @publication = N'Publication1', @frequency_type = 1;  
    EXEC sp_startpublication_snapshot @publication = N'Publication1';  
    ```  
  
2.  스냅숏 폴더로 이동합니다. 기본 위치는 "C:\Program Files\Microsoft SQL Server\MSSQL12. \<인스턴스 > \MSSQL\repldata\unc\XXX\YYYYMMDDHHMMSS\\"입니다.  
  
3.  찾을 **합니다. SCH** 테이블에 대 한 파일 및 Management Studio에서 엽니다. 아래 설명에 따라 테이블 스키마를 변경하고 저장 프로시저를 업데이트합니다.  
  
     IDX 파일에 정의된 인덱스를 평가합니다. `CREATE TABLE`을 수정하여 필수 인덱스, 제약 조건, 기본 키 및 메모리 최적화 구문을 지정합니다. 메모리 최적화 테이블에서 인덱스 열은 NOT NULL이어야 하며 문지 형식의 인덱스 열은 Unicode여야 하고 BIN2 데이터 정렬을 사용해야 합니다. 아래 예제를 참조하십시오.  
  
    ```  
    SET ANSI_PADDING ON;  
    GO  
  
    SET ANSI_NULLS ON;  
    GO  
  
    SET QUOTED_IDENTIFIER ON;  
    GO  
  
    CREATE TABLE [dbo].[Mem_Table]([c1] [int] NOT NULL,  
        [c2] [float] NOT NULL,  
        [c3] [decimal](10, 2) NOT NULL,  
        [c4] [nvarchar](5) COLLATE SQL_Latin1_General_CP850_BIN2 NOT NULL,  
        INDEX [hash_index_sample_memoryoptimizedtable_c2] HASH (c2) WITH (BUCKET_COUNT = 1024),  
        INDEX [index_sample_memoryoptimizedtable_c3] NONCLUSTERED ([c3]),  
        INDEX [nvarchar_index_sample_memoryoptimizedtable_c4] ([c4]),  
        CONSTRAINT [PK_sample_memoryoptimizedtable] PRIMARY KEY NONCLUSTERED ([c1])) WITH (MEMORY_OPTIMIZED = ON, DURABILITY = SCHEMA_AND_DATA);  
    GO  
    ```  
  
4.  `@upd_cmd` 매개 변수에 대해 SCALL 규칙을 사용할 때는 스키마(.SCH) 파일로 이동하고 `create procedure [sp_MSupd_<SCHEMA><TABLE_NAME>]`에서 테이블 업데이트 문을 변경하여 기본 키 열을 제거합니다.  
  
     기본 키 업데이트를 지원하려면 사용자 정의 업데이트 저장 프로시저를 사용해서 다음과 같이 기본 키 업데이트 문을 바꿉니다.  
  
    1.  누락된 열 값을 선택합니다(SCALL은 업데이트 작업과 관련된 열만 제공).  
  
    2.  기존 레코드를 삭제합니다.  
  
    3.  새 기본 키를 포함해서 제공된 새 값으로 새 레코드를 삽입합니다.  
  
     원래 업데이트 프로시저는 다음과 같습니다.  
  
    ```  
    create procedure [sp_MSupd_Mem_Table]  
                   @c1 int = NULL,  
                   @c2 float = NULL,  
                   @c3 decimal(10,2) = NULL,  
                   @c4 nvarchar(5) = NULL,  
                   @pkc1 int = NULL,  
                   @bitmap binary(1)  
    as  
    begin    
    if (substring(@bitmap,1,1) & 1 = 1)  
    begin   
    update [dbo].[Mem_Table] set  
                   [c1] = case substring(@bitmap,1,1) & 1 when 1 then @c1 else [c1] end,  
                   [c2] = case substring(@bitmap,1,1) & 2 when 2 then @c2 else [c2] end,  
                   [c3] = case substring(@bitmap,1,1) & 4 when 4 then @c3 else [c3] end,  
                   [c4] = case substring(@bitmap,1,1) & 8 when 8 then @c4 else [c4] end  
    where [c1] = @pkc1  
    if @@rowcount = 0  
        if @@microsoftversion>0x07320000  
            exec sp_MSreplraiserror 20598  
    end    
    else  
    begin   
    update [dbo].[Mem_Table] set  
                   [c2] = case substring(@bitmap,1,1) & 2 when 2 then @c2 else [c2] end,  
                   [c3] = case substring(@bitmap,1,1) & 4 when 4 then @c3 else [c3] end,  
                   [c4] = case substring(@bitmap,1,1) & 8 when 8 then @c4 else [c4] end  
    where [c1] = @pkc1  
    if @@rowcount = 0  
        if @@microsoftversion>0x07320000  
            exec sp_MSreplraiserror 20598  
    end   
    end   
    go  
    ```  
  
     게시자에서 기본 키를 업데이트해서는 안 되는 경우 다음과 같이 업데이트 프로시저에서 해당 열에 대한 업데이트를 주석 처리하십시오.  
  
    ```  
    create procedure [sp_MSupd_Mem_Table]  
                   @c1 int = NULL,  
                   @c2 float = NULL,  
                   @c3 decimal(10,2) = NULL,  
                   @c4 nvarchar(5) = NULL,  
                   @pkc1 int = NULL,  
                   @bitmap binary(1)  
    as  
    begin    
    if (substring(@bitmap,1,1) & 1 = 1)  
    begin   
    update [dbo].[Mem_Table] set  
    --             [c1] = case substring(@bitmap,1,1) & 1 when 1 then @c1 else [c1] end,  
                   [c2] = case substring(@bitmap,1,1) & 2 when 2 then @c2 else [c2] end,  
                   [c3] = case substring(@bitmap,1,1) & 4 when 4 then @c3 else [c3] end,  
                   [c4] = case substring(@bitmap,1,1) & 8 when 8 then @c4 else [c4] end  
    where [c1] = @pkc1  
    if @@rowcount = 0  
        if @@microsoftversion>0x07320000  
            exec sp_MSreplraiserror 20598  
    end    
    else  
    begin   
    update [dbo].[Mem_Table] set  
                   [c2] = case substring(@bitmap,1,1) & 2 when 2 then @c2 else [c2] end,  
                   [c3] = case substring(@bitmap,1,1) & 4 when 4 then @c3 else [c3] end,  
                   [c4] = case substring(@bitmap,1,1) & 8 when 8 then @c4 else [c4] end  
    where [c1] = @pkc1  
    if @@rowcount = 0  
        if @@microsoftversion>0x07320000  
            exec sp_MSreplraiserror 20598  
    end   
    end   
    go  
    ```  
  
     기본 키에 대한 업데이트 지원을 허용하려면 다음과 같이 업데이트 프로시저를 수정하십시오.  
  
    ```  
    create procedure [sp_MSupd_Mem_Table]  
                   @c1 int = NULL,  
                   @c2 float = NULL,  
                   @c3 decimal(10,2) = NULL,  
                   @c4 nvarchar(5) = NULL,  
                    @pkc1 int = NULL,  
                   @bitmap binary(1)  
    as  
    begin    
    if (substring(@bitmap,1,1) & 1 = 1)  
    begin   
    select  
                   @c1 = case substring(@bitmap,1,1) & 1 when 1 then @c1 else [c1] end,  
                   @c2 = case substring(@bitmap,1,1) & 2 when 2 then @c2 else [c2] end,  
                   @c3 = case substring(@bitmap,1,1) & 4 when 4 then @c3 else [c3] end,  
                   @c4 = case substring(@bitmap,1,1) & 8 when 8 then @c4 else [c4] end  
    from [dbo].[Mem_Table] where [c1] = @pkc1  
    if @@rowcount <> 0 begin  
            delete [dbo].[Mem_Table] where [c1] = @pkc1  
            if @@rowcount <> 0  
                   insert into [dbo].[Mem_Table]([c1],  
                           [c2],  
                           [c3],  
                           [c4]) values (  
                           @c1,  
                           @c2,  
                           @c3,  
                           @c4  
                   )   
    end  
    if @@rowcount = 0  
        if @@microsoftversion>0x07320000  
            exec sp_MSreplraiserror 20598  
    end    
    else  
    begin   
    update [dbo].[Mem_Table] set  
                   [c2] = case substring(@bitmap,1,1) & 2 when 2 then @c2 else [c2] end,  
                   [c3] = case substring(@bitmap,1,1) & 4 when 4 then @c3 else [c3] end,  
                   [c4] = case substring(@bitmap,1,1) & 8 when 8 then @c4 else [c4] end  
    where [c1] = @pkc1  
    if @@rowcount = 0  
        if @@microsoftversion>0x07320000  
            exec sp_MSreplraiserror 20598  
    end   
    end   
    go  
    ```  
  
5.  사용 하 여 구독자 데이터베이스 만들기를 **스냅숏 격리로 승격** 옵션 및 비유니코드 문자 데이터 형식을 사용 하는 경우 기본 데이터 정렬을 Latin1_General_CS_AS_KS_WS로 설정 합니다.  
  
    ```  
    CREATE DATABASE [Sub]   
    CONTAINMENT = NONE   
    ON PRIMARY ( NAME = [Sub], FILENAME = [C:\Program Files\Microsoft SQL Server\MSSQL12\MSSQL\DATA\Sub.mdf]),   
    FILEGROUP [mem] CONTAINS MEMORY_OPTIMIZED_DATA ( NAME = [mem],   
    FILENAME = [C:\Program Files\Microsoft SQL Server\MSSQL12\MSSQL\DATA\Sub])  
    LOG ON ( NAME = [Sub_log], FILENAME = [C:\Program Files\Microsoft SQL Server\MSSQL12\MSSQL\DATA\Sub.ldf])  
    COLLATE Latin1_General_CS_AS_KS_WS;  
  
    ALTER DATABASE [Sub] SET MEMORY_OPTIMIZED_ELEVATE_TO_SNAPSHOT = ON;  
    GO  
    ```  
  
6.  구독자의 데이터베이스에 스키마를 적용하고 나중에 사용할 수 있도록 스키마를 저장합니다.  
  
7.  구독자에 대해 게시자(원본) 데이터를 로드합니다. 구독을 추가할 때까지는 게시자에서 데이터가 변경되지 않아야 합니다.  아래 표시된 것처럼 BCP를 사용할 수 있습니다.  
  
    ```  
    bcp Pub.dbo.Mem_Table out Mem_Table.bcp -S. -T -C1252 -n  
    bcp Sub.dbo.Mem_Table in Mem_Table.bcp -S. -T -C1252 -n  
    ```  
  
8.  구독자에서 스키마 변경을 사용하지 않도록 아티클을 다시 구성합니다.  
  
    ```  
    EXEC sp_changearticle  
        @publication = N'Publication1',  
        @article = N'Mem_Table',  
        @property = N'schema_option',  
        @value = 0,  
        @force_invalidate_snapshot = 1,  
        @force_reinit_subscription = 1;  
    GO  
    ```  
  
 **비동기 구독 추가**  
  
 비동기 구독을 추가합니다.  
  
```  
EXEC sp_addsubscription  
    @publication = N' Publication1',  
    @subscriber = @@ServerName,  
    @destination_db = N'Sub',  
    @subscription_type = N'Push',  
    @sync_type = N'replication support only',  
    @article = N'all',  
    @update_mode = N'read only',  
    @subscriber_type = 0;  
GO  
```  
  
 메모리 액세스에 최적화된 테이블이 이제 게시자로부터 업데이트 수신을 시작합니다.  
  
## <a name="restrictions"></a>Restrictions  
 단방향 트랜잭션 복제만 지원됩니다. 피어 투 피어 트랜잭션 복제는 지원되지 않습니다.  
  
 메모리 액세스에 최적화된 테이블은 게시할 수 없습니다.  
  
 배포자의 복제 테이블은 메모리 최적화 테이블로 구성할 수 없습니다.  
  
 병합 복제는 메모리 최적화 테이블을 포함할 수 없습니다.  
  
 구독자에서 트랜잭션 복제와 관련된 테이블은 메모리 최적화 테이블로 구성할 수 있지만 구독자 테이블은 메모리 최적화 테이블의 요구 사항을 충족해야 합니다. 여기에는 다음과 같은 제한 사항이 필요합니다.  
  
-   트랜잭션 복제 구독자에서 메모리 최적화 테이블을 만들려면 메모리 최적화 테이블을 만드는 데 사용된 스냅숏 스키마 파일을 수동으로 수정해야 합니다. 자세한 내용은 [스키마 파일 수정](#Schema)합니다.  
  
-   구독자에서 메모리 최적화 테이블로 복제된 테이블은 메모리 최적화 테이블의 행당 8060바이트로 제한됩니다.  
  
-   구독자에서 메모리 최적화 테이블로 복제된 테이블은 메모리 최적화 테이블에 허용된 데이터 형식으로 제한됩니다. 자세한 내용은 [Supported Data Types](../in-memory-oltp/supported-data-types-for-in-memory-oltp.md)합니다.  
  
-   구독자에서 메모리 최적화 테이블에 복제하는 테이블의 기본 키는 업데이트하는 데 제한 사항이 있습니다. 자세한 내용은 [기본 키에 변경 내용 복제](#PrimaryKey)합니다.  
  
-   외래 키, 고유 제약 조건, 트리거, 스키마 수정, ROWGUIDCOL, 계산 열, 데이터 압축, 별칭 데이터 형식, 버전 관리 및 잠금은 메모리 최적화 테이블에서 지원되지 않습니다. 참조 [TRANSACT-SQL에서 메모리 내 OLTP에서 지원 되지 않는 구문](../in-memory-oltp/transact-sql-constructs-not-supported-by-in-memory-oltp.md) 정보에 대 한 합니다.  
  
##  <a name="Schema"></a> 스키마 파일 수정  
  
-   클러스터형 인덱스는 지원되지 않습니다. 클러스터형 인덱스를 비클러스터형 인덱스로 변경합니다.  
  
-   인덱스의 키에서 모든 열은 `NOT NULL`로 지정되어야 합니다.  
  
-   메모리 최적화 테이블 옵션 `DURABILITY = SCHEMA_AND_DATA`를 사용할 경우 테이블은 비클러스터형 기본 키 인덱스를 포함해야 합니다.  
  
-   ANSI_PADDING은 ON이어야 합니다.  
  
##  <a name="PrimaryKey"></a> 기본 키에 변경 내용 복제  
 메모리 최적화 테이블의 기본 키는 업데이트할 수 없습니다. 구독자에서 기본 키 업데이트를 복제하려면 삭제 및 삽입 쌍으로 업데이트를 제공하도록 업데이트 저장 프로시저를 수정합니다.  
  
## <a name="see-also"></a>관련 항목  
 [복제 기능 및 태스크](replication-features-and-tasks.md)  
  
  
