---
title: OLE 자동화 반환 코드 및 오류 정보 | Microsoft 문서
ms.custom: ''
ms.date: 07/05/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: stored-procedures
ms.topic: conceptual
helpviewer_keywords:
- return codes [SQL Server]
- OLE Automation [SQL Server], return codes
- OLE Automation [SQL Server], errors
ms.assetid: 9696fb05-e9e8-4836-b359-d4de0be0eeb2
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 5f16c6d9d410cf9a7928d5ff9b1d2629578f3e84
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47779571"
---
# <a name="ole-automation-return-codes-and-error-information"></a>OLE Automation 반환 코드 및 오류 정보
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
  OLE 자동화 시스템 저장 프로시저는 기본 OLE 자동화 작업에 의해 반환되는 HRESULT를 **int** 반환 코드로 반환합니다. HRESULT 값이 0이면 성공을 나타냅니다. 0이 아닌 HRESULT는 0x800*nnnnn*과 같은 16진수 형태의 OLE 오류 코드이고, 저장 프로시저 반환 코드에서 **int** 값으로 반환된 경우에는 HRESULT의 형태가 214*nnnnnnn*입니다.  
  
 예를 들어 잘못된 개체 이름(SQLDMO.Xyzzy)을 sp_OACreate에 전달하면 프로시저는 16진수로 0x800401f3인 2147221005의 **int** HRESULT를 반환합니다.  
  
 `CONVERT(binary(4), @hresult)` 를 사용하여 **int** HRESULT를 **binary** 값으로 변환할 수 있습니다. 그러나 `CONVERT(char(10), CONVERT(binary(4), @hresult))` 를 사용하면 HRESULT의 각 바이트가 하나의 ASCII 문자로 변환되어 알아볼 수 없는 문자열이 됩니다. 다음 예제 HexToChar 저장 프로시저를 사용하면 **int** HRESULT를 알아볼 수 있는 16진수 문자열이 포함된 **char** 값으로 변환할 수 있습니다.  
  
```  
USE AdventureWorks2012;  
GO  
IF EXISTS(SELECT name FROM sys.objects  
          WHERE name = N'dbo.sp_HexToChar')  
    DROP PROCEDURE HexToChar;  
GO  
CREATE PROCEDURE dbo.sp_HexToChar  
    @BinValue varbinary(255),  
    @HexCharValue nvarchar(255) OUTPUT  
AS  
    DECLARE @CharValue nvarchar(255);  
    DECLARE @Position int;  
    DECLARE @Length int;  
    DECLARE @HexString nchar(16);  
    SELECT @CharValue = N'0x';  
    SELECT @Position = 1;  
    SELECT @Length = DATALENGTH(@BinValue);  
    SELECT @HexString = N'0123456789ABCDEF';  
    WHILE (@Position <= @Length)  
    BEGIN  
        DECLARE @TempInt int;  
        DECLARE @FirstInt int;  
        DECLARE @SecondInt int;  
        SELECT @TempInt = CONVERT(int, SUBSTRING(@BinValue,@Position,1));  
        SELECT @FirstInt = FLOOR(@TempInt/16);  
        SELECT @SecondInt = @TempInt - (@FirstInt*16);  
        SELECT @CharValue = @CharValue +  
            SUBSTRING(@HexString, @FirstInt+1, 1) +  
            SUBSTRING(@HexString, @SecondInt+1, 1);  
        SELECT @Position = @Position + 1;  
    END  
    SELECT @HexCharValue = @CharValue;  
GO  
DECLARE @BinVariable varbinary(35);  
DECLARE @CharValue nvarchar(35);  
  
SET @BinVariable = 123456;  
  
EXECUTE dbo.sp_HexToChar  
    @binvalue = @BinVariable,  
    @HexCharValue = @CharValue OUTPUT;  
  
SELECT @BinVariable AS BinaryValue,  
    @CharValue AS CharacterRep;  
GO  
```  
  
 다음 예제 **sp_displayoaerrorinfo** 저장 프로시저를 사용하면 OLE 자동화 프로시저 중 하나가 0이 아닌 HRESULT 반환 코드를 반환할 때 OLE 자동화 오류 정보를 표시할 수 있습니다. 다음 예제 저장 프로시저는 **HexToChar**를 사용합니다.  
  
```  
CREATE PROCEDURE dbo.sp_DisplayOAErrorInfo  
    @Object int,  
    @HResult int  
AS  
    DECLARE @Output nvarchar(255);  
    DECLARE @HRHex nchar(10);  
    DECLARE @HR int;  
    DECLARE @Source nvarchar(255);  
    DECLARE @Description nvarchar(255);  
    PRINT N'OLE Automation Error Information';  
    EXEC sp_HexToChar @HResult, @HRHex OUT;  
    SELECT @Output = N'  HRESULT: ' + @HRHex;  
    PRINT @Output;  
    EXEC @HR = sp_OAGetErrorInfo  
        @Object,  
        @Source OUT,  
        @Description OUT;  
    IF @HR = 0  
    BEGIN  
        SELECT @Output = N'  Source: ' + @Source;  
        PRINT @Output;  
        SELECT @Output = N'  Description: '  
               + @Description;  
        PRINT @Output;  
    END  
    ELSE  
    BEGIN  
       PRINT N' sp_OAGetErrorInfo failed.';  
       RETURN;  
    END  
GO  
```  
  
## <a name="related-content"></a>관련 내용  
 [sp_OAGetErrorInfo&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-oageterrorinfo-transact-sql.md)  
  
  
