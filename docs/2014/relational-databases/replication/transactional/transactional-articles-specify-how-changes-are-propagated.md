---
title: 트랜잭션 아티클에 대한 변경 내용을 전파하는 방법 지정 | Microsoft 문서
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- transactional replication, propagation methods
ms.assetid: a10c5001-22cc-4667-8f0b-3d0818dca2e9
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: de28a4353c5d690e30cd2cefc20f50e4911c6ff1
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "62655678"
---
# <a name="specify-how-changes-are-propagated-for-transactional-articles"></a>트랜잭션 아티클에 대한 변경 내용을 전파하는 방법 지정
  트랜잭션 복제를 사용하여 데이터 변경 내용이 게시자에서 구독자로 전파되는 방법을 지정할 수 있습니다. 다음 4가지 중 하나를 사용하여 게시된 각 테이블에 대해 INSERT, UPDATE 또는 DELETE 등의 각 작업이 구독자로 전파되는 방법을 지정할 수 있습니다.  
  
-   트랜잭션 복제가 저장 프로시저를 스크립팅한 후 저장 프로시저를 호출하여 변경 내용을 구독자로 전파하도록 지정합니다(기본값).  
  
-   INSERT, UPDATE 또는 DELETE 문을 사용하여 변경 내용을 전파하도록 지정합니다.[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 이외 구독자인 경우 기본값입니다.  
  
-   사용자 지정 저장 프로시저를 사용하도록 지정합니다.  
  
-   어떤 구독자도 이 동작을 수행하지 않도록 지정합니다. 해당 유형의 트랜잭션은 복제되지 않습니다.  
  
 기본적으로 트랜잭션 복제는 각 구독자에 설치된 저장 프로시저 집합를 통하여 변경 내용을 구독자로 전파합니다. 게시자의 테이블에서 삽입, 업데이트 또는 삭제 작업이 발생하면 이러한 작업은 구독자에서 저장 프로시저에 대한 호출로 변환됩니다. 저장 프로시저에서는 테이블의 열로 매핑하는 매개 변수를 적용하여 이러한 열이 구독자에서 변경되도록 합니다.  
  
 트랜잭션 아티클의 데이터 변경 내용을 전파하는 방법을 설정하려면 [트랜잭션 아티클의 데이터 변경 내용을 전파하는 방법 설정](../publish/set-the-propagation-method-for-data-changes-to-transactional-articles.md)을 참조하십시오.  
  
## <a name="default-and-custom-stored-procedures"></a>기본 저장 프로시저 및 사용자 지정 저장 프로시저  
 복제 시 각 테이블 아티클에 대해 기본적으로 생성되는 3가지 프로시저는 다음과 같습니다.  
  
-   **sp_MSins_\<** *tablename* **>** - 삽입을 처리합니다.  
  
-   **sp_MSupd_\<** *tablename* **>** - 업데이트를 처리합니다.  
  
-   **sp_MSdel_\<** *tablename* **>** - 삭제를 처리합니다.  
  
 프로시저에서 사용하는 **\< ***tablename ***>** 은 아티클을 게시에 추가하는 방법과 구독 데이터베이스에 소유자는 다르지만 이름이 같은 테이블이 포함되어 있는지 여부에 따라 다릅니다.  
  
 이러한 프로시저는 아티클을 게시에 추가할 때 지정하는 사용자 지정 프로시저로 바꿀 수 있습니다. 구독자에서 행이 업데이트될 때 데이터를 감사 테이블에 삽입하는 경우와 같이 애플리케이션에 사용자 지정 논리가 필요할 경우 사용자 지정 프로시저를 사용합니다. 사용자 지정 저장 프로시저 지정 방법은 위에 나열된 항목을 참조하십시오.  
  
 기본 복제 프로시저 또는 사용자 지정 프로시저를 지정하면 각 프로시저에 대한 호출 구문도 지정해야 합니다. 기본 프로시저를 사용할 경우에는 복제에서 기본값을 선택합니다. 호출 구문은 프로시저에 제공되는 매개 변수의 구조 및 각 데이터 변경 시 구독자로 보낼 정보의 양을 결정합니다. 자세한 내용은 이 항목의 "저장 프로시저 호출 구문" 섹션을 참조하십시오.  
  
### <a name="considerations-for-using-custom-stored-procedures"></a>사용자 지정 저장 프로시저 사용 시 고려 사항  
 사용자 지정 저장 프로시저를 사용할 때는 다음 사항을 고려하십시오.  
  
-   [!INCLUDE[msCoName](../../../includes/msconame-md.md)] 에서는 사용자 지정 논리를 지원하지 않으므로 사용자가 저장 프로시저의 논리를 지원해야 합니다.  
  
-   복제에서 사용하는 트랜잭션과 충돌을 피하려면 사용자 지정 프로시저에서 명시적 트랜잭션을 사용하지 않아야 합니다.  
  
-   일반적으로 구독자에 있는 스키마는 게시자에 있는 스키마는 동일하지만 열 필터링을 사용할 경우 게시자 스키마의 하위 집합일 수도 있습니다. 데이터를 이동할 때 구독자에 있는 스키마가 게시자에 있는 스키마의 하위 집합이 되지 않도록 스키마를 변환하려면 [!INCLUDE[ssISCurrent](../../../includes/ssiscurrent-md.md)] 를 사용하는 것이 좋습니다. 자세한 내용은 [SQL Server Integration Services](../../../integration-services/sql-server-integration-services.md)를 참조하세요.  
  
-   게시된 테이블에 대해 스키마 변경을 적용하면 사용자 지정 프로시저를 다시 생성해야 합니다. 자세한 내용은 [스키마 변경 내용을 반영하기 위해 사용자 지정 트랜잭션 프로시저 다시 생성](transactional-articles-regenerate-to-reflect-schema-changes.md)을 참조하세요.  
  
-   배포 에이전트의 **-SubscriptionStreams** 매개 변수에 1보다 큰 값을 사용할 경우 기본 키 열에 대한 업데이트가 성공했는지 확인해야 합니다. 다음은 그 예입니다.  
  
    ```  
    update ... set pk = 2 where pk = 1 -- update 1  
    update ... set pk = 3 where pk = 2 -- update 2  
    ```  
  
     배포 에이전트에서 두 개 이상의 연결을 사용할 경우 이러한 두 업데이트를 서로 다른 연결을 통해 복제할 수 있습니다. 업데이트 1이 먼저 적용되면 아무 문제 없지만 업데이트 2가 먼저 적용되면 업데이트 1이 아직 적용되지 않았기 때문에 '적용된 행 없음' 메시지가 반환됩니다. 기본 프로시저에서는 업데이트 시 변경된 행이 없을 경우 오류를 발생시켜 이 상황을 처리합니다.  
  
    ```  
    if @@rowcount = 0  
        if @@microsoftversion>0x07320000  
            exec sys.sp_MSreplraiserror 20598  
    ```  
  
     오류가 발생하면 배포 에이전트가 단일 연결을 통해 업데이트를 다시 시도하고 이로 인해 업데이트가 성공적으로 수행됩니다. 사용자 지정 저장 프로시저에도 비슷한 논리가 포함되어야 합니다.  
  
### <a name="call-syntax-for-stored-procedures"></a>저장 프로시저 호출 구문  
 트랜잭션 복제에서 사용하는 프로시저를 호출하는 데 사용되는 구문은 5개가 있습니다.  
  
-   CALL 구문. 삽입, 업데이트 및 삭제에 사용할 수 있습니다. 기본적으로 복제에서는 이 구문을 삽입 및 삭제에 사용합니다.  
  
-   SCALL 구문. 업데이트에만 사용할 수 있습니다. 기본적으로 복제에서는 이 구문을 업데이트에 사용합니다.  
  
-   MCALL 구문. 업데이트에만 사용할 수 있습니다.  
  
-   XCALL 구문. 업데이트 및 삭제에 사용할 수 있습니다.  
  
-   VCALL 구문. 업데이트할 수 있는 구독에 사용합니다. 내부적으로만 사용됩니다.  
  
 각 방법은 구독자로 전파되는 데이터 양에 차이가 있습니다. 예를 들어 SCALL은 실제로 업데이트가 적용된 열 값만 전달합니다. 이와 대조적으로 XCALL은 업데이트 적용 여부에 상관없이 모든 열 및 각 열에 대한 모든 이전 데이터 값이 필요합니다. 대부분의 경우 업데이트에는 SCALL이 적합하지만 애플리케이션에서 업데이트하는 동안 모든 데이터를 필요로 하는 경우에는 XCALL이 적합합니다.  
  
#### <a name="call-syntax"></a>CALL 구문  
 INSERT 저장 프로시저  
 INSERT 문을 처리하는 저장 프로시저는 모든 열에 대해 삽입된 값을 전달합니다.  
  
```  
c1, c2, c3,... cn  
```  
  
 UPDATE 저장 프로시저  
 UPDATE 문을 처리하는 저장 프로시저에 아티클에 정의된 모든 열에 대해 업데이트된 값이 전달된 다음 기본 키 열의 원래 값이 전달됩니다. 변경된 열은 확인하지 않습니다.  
  
```  
c1, c2, c3,... cn, pkc1, pkc2, pkc3,... pkcn  
```  
  
 DELETE 저장 프로시저  
 DELETE 문을 처리하는 저장 프로시저에 기본 키 열에 대한 값이 전달됩니다.  
  
```  
pkc1, pkc2, pkc3,... pkcn  
```  
  
#### <a name="scall-syntax"></a>SCALL 구문  
 UPDATE 저장 프로시저  
 변경된 열에 대해서만 UPDATE 문을 처리하는 저장 프로시저에 업데이트된 값이 전달된 다음 차례대로 기본 키 열의 원래 값과 변경된 열을 나타내는 비트 마스크(`binary(n)`) 매개 변수가 전달됩니다. 다음 예에서 열 2(c2)는 변경되지 않은 것입니다.  
  
```  
c1, , c3,... cn, pkc1, pkc2, pkc3,... pkcn, bitmask  
```  
  
#### <a name="mcall-syntax"></a>MCALL 구문  
 UPDATE 저장 프로시저  
 UPDATE 문을 처리하는 저장 프로시저에 아티클에 정의된 모든 열에 대해 업데이트된 값이 전달된 다음 차례대로 기본 키 열의 원래 값과 변경된 열을 나타내는 비트 마스크(`binary(n)`) 매개 변수가 전달됩니다.  
  
```  
c1, c2, c3,... cn, pkc1, pkc2, pkc3,... pkcn, bitmask  
```  
  
#### <a name="xcall-syntax"></a>XCALL 구문  
 UPDATE 저장 프로시저  
 UPDATE 문을 처리하는 저장 프로시저에 아티클에 정의된 모든 열에 대한 원래 값(이전 이미지)이 전달된 다음 아티클에 정의된 모든 열의 업데이트 값(이후 이미지)이 전달됩니다.  
  
```  
old-c1, old-c2, old-c3,... old-cn, c1, c2, c3,... cn,  
```  
  
 DELETE 저장 프로시저  
 DELETE 문을 처리하는 저장 프로시저에 아티클에 정의된 모든 열에 대한 원래 값(이전 이미지)이 전달됩니다.  
  
```  
old-c1, old-c2, old-c3,... old-cn  
```  
  
> [!NOTE]  
>  XCALL을 사용하는 경우 **text** 및 **image** 열에 대한 이전 이미지 값은 NULL이 됩니다.  
  
## <a name="examples"></a>예  
 다음 프로시저는 `Vendor Table` 예제 데이터베이스의 [!INCLUDE[ssSampleDBCoShort](../../../includes/sssampledbcoshort-md.md)] 용으로 만든 기본 프로시저입니다.  
  
```  
--INSERT procedure using CALL syntax  
create procedure [sp_MSins_PurchasingVendor]   
  @c1 int,@c2 nvarchar(15),@c3 nvarchar(50),@c4 tinyint,@c5 bit,@c6 bit,@c7 nvarchar(1024),@c8 datetime  
as   
begin   
insert into [Purchasing].[Vendor]([VendorID]  
,[AccountNumber]  
,[Name]  
,[CreditRating]  
,[PreferredVendorStatus]  
,[ActiveFlag]  
,[PurchasingWebServiceURL]  
,[ModifiedDate])  
values (   
 @c1  
,@c2  
,@c3  
,@c4  
,@c5  
,@c6  
,@c7  
,@c8  
 )   
end  
go  
  
--UPDATE procedure using SCALL syntax  
create procedure [sp_MSupd_PurchasingVendor]   
 @c1 int = null,@c2 nvarchar(15) = null,@c3 nvarchar(50) = null,@c4 tinyint = null,@c5 bit = null,@c6 bit = null,@c7 nvarchar(1024) = null,@c8 datetime = null,@pkc1 int  
,@bitmap binary(2)  
as  
begin  
update [Purchasing].[Vendor] set   
 [AccountNumber] = case substring(@bitmap,1,1) & 2 when 2 then @c2 else [AccountNumber] end  
,[Name] = case substring(@bitmap,1,1) & 4 when 4 then @c3 else [Name] end  
,[CreditRating] = case substring(@bitmap,1,1) & 8 when 8 then @c4 else [CreditRating] end  
,[PreferredVendorStatus] = case substring(@bitmap,1,1) & 16 when 16 then @c5 else [PreferredVendorStatus] end  
,[ActiveFlag] = case substring(@bitmap,1,1) & 32 when 32 then @c6 else [ActiveFlag] end  
,[PurchasingWebServiceURL] = case substring(@bitmap,1,1) & 64 when 64 then @c7 else [PurchasingWebServiceURL] end  
,[ModifiedDate] = case substring(@bitmap,1,1) & 128 when 128 then @c8 else [ModifiedDate] end  
where [VendorID] = @pkc1  
if @@rowcount = 0  
    if @@microsoftversion>0x07320000  
        exec sp_MSreplraiserror 20598  
end  
go  
  
--DELETE procedure using CALL syntax  
create procedure [sp_MSdel_PurchasingVendor]   
  @pkc1 int  
as   
begin   
delete [Purchasing].[Vendor]  
where [VendorID] = @pkc1  
if @@rowcount = 0  
    if @@microsoftversion>0x07320000  
        exec sp_MSreplraiserror 20598  
end   
go  
```  
  
## <a name="see-also"></a>참고 항목  
 [Article Options for Transactional Replication](article-options-for-transactional-replication.md)  
  
  
