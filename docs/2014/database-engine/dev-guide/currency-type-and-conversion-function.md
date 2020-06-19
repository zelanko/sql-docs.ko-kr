---
title: 통화 형식 및 변환 함수 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: reference
ms.assetid: df516567-8689-45c2-b418-16473f8d43e4
author: mashamsft
ms.author: mathoma
ms.openlocfilehash: fb4a2b48343c6424007a590f7a54e40290c6a345
ms.sourcegitcommit: 9ee72c507ab447ac69014a7eea4e43523a0a3ec4
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/17/2020
ms.locfileid: "84933657"
---
# <a name="currency-type-and-conversion-function"></a>통화 형식 및 변환 함수
  이 예에서는 C#을 사용하여 Currency 사용자 정의 데이터 형식을 정의합니다. 이 사용자 정의 데이터 형식에서는 금액과 culture를 모두 캡슐화하여 금액을 해당 culture의 통화 값으로 렌더링하는 올바른 방법을 결정하는 데 도움을 줍니다. 이 예에서는 Currency 사용자 정의 데이터 형식의 인스턴스를 반환하는 통화 변환 함수도 제공합니다. AdventureWorks 데이터베이스에 미국 달러(USD)를 지정된 culture와 연관된 통화로 변환하는 환율이 있는 경우 변환 함수는 변환된 환율 및 요청 culture와 일치하는 culture와 함께 Currency 사용자 정의 데이터 형식을 반환합니다. 그렇지 않으면 Currency 사용자 정의 데이터 형식은 `en-us` culture인 미국 달러(USD) 단위의 원래 금액과 함께 반환됩니다. 이 예에서는 Transact-SQL을 사용하여 CLR(공용 언어 런타임) 메서드 및 어셈블리를 등록 및 등록 해제하는 방법도 보여 줍니다.  
  
> [!CAUTION]  
>  이 예제에서 사용하는 환율은 실제 환율이 아니므로 실제 금융 거래에 사용할 수 없습니다.  
  
## <a name="prerequisites"></a>사전 요구 사항  
 이 프로젝트를 만들고 실행하려면 다음 소프트웨어가 설치되어 있어야 합니다.  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 또는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Express [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Express는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Express 설명서 및 예제 [웹 사이트](https://www.microsoft.com/sql-server/sql-server-editions-express)에서 무료로 구할 수 있습니다.  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 개발자 [웹 사이트](https://go.microsoft.com/fwlink/?linkid=62796)에서 제공되는 AdventureWorks 데이터베이스  
  
-   .NET Framework SDK 2.0 이상 또는 Microsoft Visual Studio 2005 이상. .NET Framework SDK는 무료로 구할 수 있습니다.  
  
-   또한 다음 조건을 충족해야 합니다.  
  
-   사용하고 있는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스에 대해 CLR 통합이 설정되어 있어야 합니다.  
  
-   CLR 통합을 설정하려면 다음 단계를 수행합니다.  
  
    #### <a name="enabling-clr-integration"></a>CLR 통합 사용  
  
    -   다음 [!INCLUDE[tsql](../../includes/tsql-md.md)] 명령을 실행합니다.  
  
     `sp_configure 'clr enabled', 1`  
  
     `GO`  
  
     `RECONFIGURE`  
  
     `GO`  
  
    > [!NOTE]  
    >  CLR을 사용하도록 설정하려면 `ALTER SETTINGS` 서버 수준 사용 권한이 있어야 합니다. 이 사용 권한은 `sysadmin` 및 `serveradmin` 고정 서버 역할의 멤버가 암시적으로 소유합니다.  
  
-   사용하고 있는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스에 AdventureWorks 데이터베이스를 설치해야 합니다.  
  
-   사용하고 있는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스의 관리자가 아닌 경우 설치를 완료하기 위해 관리자로부터 **CreateAssembly** 권한을 부여 받아야 합니다.  
  
## <a name="building-the-sample"></a>예제 빌드  
  
#### <a name="create-and-run-the-sample-by-using-the-following-instructions"></a>다음 지침을 사용하여 예제를 만들고 실행합니다.  
  
1.  Visual Studio 또는 .NET Framework 명령 프롬프트를 엽니다.  
  
2.  필요한 경우 예제에 대한 디렉터리를 만듭니다. 이 예에서는 C:\MySample을 사용합니다.  
  
3.  c:\MySample에서 `Currency.cs`를 만들고 C# 예제 코드(아래)를 파일에 복사합니다.  
  
4.  다음을 실행하여 명령줄 프롬프트에서 예제 코드를 컴파일합니다.  
  
    -   `Csc /reference:C:\Windows\Microsoft.NET\Framework\v2.0.50727\System.Data.dll /reference:C:\Windows\Microsoft.NET\Framework\v2.0.50727\System.dll /reference:C:\Windows\Microsoft.NET\Framework\v2.0.50727\System.Xml.dll  /target:library Currency.cs`  
  
5.  [!INCLUDE[tsql](../../includes/tsql-md.md)] 설치 코드를 파일에 복사하고 해당 파일을 예제 디렉터리에 `Install.sql` 로 저장합니다.  
  
6.  예제가 `C:\MySample\`이외의 디렉터리에 설치된 경우 해당 위치를 가리키도록 표시된 대로 `Install.sql` 파일을 편집합니다.  
  
7.  다음을 실행하여 어셈블리 및 저장 프로시저를 배포합니다.  
  
    -   `sqlcmd -E -I -i install.sql`  
  
8.  [!INCLUDE[tsql](../../includes/tsql-md.md)] 테스트 명령 스크립트를 파일에 복사하고 해당 파일을 예제 디렉터리에 `test.sql` 로 저장합니다.  
  
9. 다음 명령으로 테스트 스크립트를 실행합니다.  
  
    -   `sqlcmd -E -I -i test.sql`  
  
10. [!INCLUDE[tsql](../../includes/tsql-md.md)] 정리 스크립트를 파일에 복사하고 해당 파일을 예제 디렉터리에 `cleanup.sql` 로 저장합니다.  
  
11. 다음 명령으로 스크립트를 실행합니다.  
  
    -   `sqlcmd -E -I -i cleanup.sql`  
  
## <a name="sample-code"></a>샘플 코드  
 다음은 이 예제에 대한 코드 목록입니다.  
  
 C#  
  
```  
using System;  
using System.Globalization;  
using System.Data.SqlTypes;  
using Microsoft.SqlServer.Server;  
using System.Data;  
using System.Data.Sql;  
using System.IO;  
using System.Data.SqlClient;  
  
    /// <summary>  
    ///Defines a class for handing particular amounts of money in a   
    ///particular culture's monetary system.  This class is exposed as   
    ///a SQL Server UDT.  
///   
///Note that we are implementing IComparable to affect comparison behavior   
///only within the CLR.  This does not affect how SQL Server will compare the  
///     the types.  How SQL Server will compare the type is determined by the Write   
///method on IBinarySerialize.  
    /// </summary>  
[Serializable]  
    [SqlUserDefinedType(Format.UserDefined, IsByteOrdered = true, MaxByteSize = 32)]  
    public struct Currency : INullable, IComparable, IBinarySerialize  
    {  
        const string nullMarker = "\0\0\0\0\0\0\0\0\0\0";  
        const int cultureNameMaxSize = 10;  
  
        private string cultureName;//Who issued the money (en-us, for example)  
  
        private CultureInfo culture;//The object which represents cultureName  
  
        private decimal currencyValue;//The amount of money  
  
        // Public properties for private fields  
        public CultureInfo Culture  
        {  
            get  
            {  
                //A culture name is required.  If not present the entire object is considered null.  
                if (cultureName == null) return null;  
  
                //If we've got a cached copy of the culture return it.  
                if (culture != null) return culture;  
  
                //Otherwise, set the cache and return the culture for the culture name specified.  
                culture = CultureInfo.CreateSpecificCulture(cultureName);  
                return culture;  
            }  
        }  
  
        // Public property for the private field.  
        public decimal CurrencyValue  
        {  
            get  
            {  
                return currencyValue;  
            }  
        }  
  
        // Constructors for when we have the culture or the name of the culture  
  
        public Currency(CultureInfo culture, decimal currencyValue)  
        {  
if (culture == null) throw new ArgumentNullException("culture");  
            this.cultureName = culture.Name;  
            this.culture = culture;  
            this.currencyValue = currencyValue;  
        }  
  
        public Currency(string cultureName, decimal currencyValue)  
        {  
            this.cultureName = cultureName;  
            this.culture = null;  
            this.currencyValue = currencyValue;  
        }  
  
        //Return the string representation for the currency, including the currency symbol.  
        [SqlMethod(IsDeterministic = true,  
            IsPrecise = true, DataAccess = DataAccessKind.None,  
            SystemDataAccess = SystemDataAccessKind.None)]  
        public override string ToString()  
        {  
            if (this.Culture == null) return "null";  
  
            return String.Format(this.Culture, "{0:c}", currencyValue);  
        }  
  
        //The entire value of the currency is considered null if the culture name is null  
        public bool IsNull  
        {  
            get  
            {  
                return cultureName == null;  
            }  
        }  
  
        //The no-argument constructor makes a null currency.  
        public static Currency Null  
        {  
            get  
            {  
                Currency h = new Currency((String)null, 0);  
  
                return h;  
            }  
        }  
  
        //Be sure to set the current UI culture before using this method! Even better, provide the culture  
        //specifically (for the method after this one).  
        [SqlMethod(IsDeterministic = true, IsPrecise = true, DataAccess = DataAccessKind.None, SystemDataAccess = SystemDataAccessKind.None)]  
        public static Currency Parse(SqlString sqlString)  
        {  
            return ParseWithCulture(sqlString, CultureInfo.CurrentUICulture);  
        }  
  
        public static Currency ParseWithCulture(SqlString sqlString, CultureInfo culture)  
        {  
            if (sqlString.IsNull   
|| (string.Compare(sqlString.Value, "null", true, CultureInfo.CurrentUICulture) == 0))  
                return Currency.Null;  
  
            int digitPos = -1;  
            string stringValue = sqlString.Value;  
  
            while (digitPos < stringValue.Length   
                && !Char.IsDigit(stringValue, ++digitPos))  
            {  
            }  
  
            if (digitPos < stringValue.Length)  
                return new Currency(culture, decimal.Parse(  
                    stringValue.Substring(digitPos), culture));  
  
            return Currency.Null;  
        }  
  
        public override int GetHashCode()  
        {  
            if (this.IsNull)  
                return 0;  
  
            return this.ToString().GetHashCode();  
        }  
  
//Note: This only affects the behavior of CLR, not SQL Server.  Comparisions  
//for SQL Server will be determined by the Write method below.  
  
public int CompareTo(object obj)  
        {  
            if (obj == null)  
                return 1; //by definition  
  
            if (obj == null || !(obj is Currency))  
                throw new ArgumentException(  
                    "the argument to compare is not a Currency");  
  
            Currency c = (Currency)obj;  
  
            if (this.IsNull)  
            {  
                if (c.IsNull)  
                    return 0;  
  
                return -1;  
            }  
  
            if (c.IsNull)  
                return 1;  
  
            string thisCultureName = this.Culture.Name;  
            string otherCultureName = c.Culture.Name;  
            if (!thisCultureName.Equals(otherCultureName))  
                return thisCultureName.CompareTo(otherCultureName);  
            return this.CurrencyValue.CompareTo(c.CurrencyValue);  
        }  
        // IBinarySerialize methods  
        // The binary layout is as follow:  
        //    Bytes 0 - 19:Culture name, padded to the right with null characters, UTF-16 encoded  
        //    Bytes 20+:Decimal value of money  
        // If the culture name is empty, the currency is null.  
  
        public void Write(System.IO.BinaryWriter w)  
        {  
if (w == null) throw new ArgumentNullException("w");  
            if (this.IsNull)  
            {  
                w.Write(nullMarker);  
                w.Write((decimal)0);  
                return;  
            }  
  
            if (cultureName.Length > cultureNameMaxSize)  
            {  
                throw new ApplicationException(string.Format(  
                    CultureInfo.InvariantCulture,   
                    "{0} is an invalid culture name for currency as it is too long.",   
                    cultureNameMaxSize));  
            }  
  
            String paddedName = cultureName.PadRight(cultureNameMaxSize, '\0');  
            for (int i = 0; i < cultureNameMaxSize; i++)  
            {  
                w.Write(paddedName[i]);  
            }  
  
            // Normalize decimal value to two places  
            currencyValue = Decimal.Floor(currencyValue * 100) / 100;  
            w.Write(currencyValue);  
        }  
        public void Read(System.IO.BinaryReader r)  
        {  
            char[] name = r.ReadChars(cultureNameMaxSize);  
            int stringEnd = Array.IndexOf(name, '\0');  
  
            if (stringEnd == 0)  
            {  
                cultureName = null;  
                return;  
            }  
  
            cultureName = new String(name, 0, stringEnd);  
            currencyValue = r.ReadDecimal();  
        }  
    }  
  
    /// <summary>  
    /// This class is used to compute the value of US money a given region.  
    /// </summary>  
    public sealed class CurrencyConverter  
    {  
        // Classes with only static members should not be instantiable  
        private CurrencyConverter()  
        {  
        }  
  
        private static readonly CultureInfo USCulture = CultureInfo.CreateSpecificCulture("en-us");  
  
        /// <summary>  
        ///Computes the value of a certain amount of money in the USA in a different region.  
        /// </summary>  
        /// <param name="fromAmount">The quantity of money</param>  
        /// <param name="toCultureName">A culture which is a member of the region of interest</param>  
        /// <returns></returns>  
        [Microsoft.SqlServer.Server.SqlFunction(IsDeterministic = true, DataAccess = Microsoft.SqlServer.Server.DataAccessKind.Read)]  
        public static Currency ConvertCurrency(SqlMoney fromAmount, SqlString toCultureName, SqlDateTime when)  
        {  
            CultureInfo toCulture = CultureInfo.CreateSpecificCulture(toCultureName.Value);  
  
            if (toCulture.Equals(USCulture))  
            {  
                Currency c = new Currency(USCulture, (decimal)fromAmount);  
                return c;  
            }  
  
            String toCurrencyCode = new RegionInfo(toCulture.LCID).ISOCurrencySymbol;  
  
            // Find the rate closest to the specified date  
  
            using (SqlConnection conn = new SqlConnection("context connection=true"))  
            {  
  
                SqlCommand command = conn.CreateCommand();  
                command.CommandType = CommandType.StoredProcedure;  
                command.CommandText = "usp_LookupConversionRate";  
  
                SqlParameter onDateParameter  
                    = new SqlParameter("@OnDate", SqlDbType.DateTime);  
                onDateParameter.Value = when;  
                command.Parameters.Add(onDateParameter);  
  
                SqlParameter toCurrencyCodeParameter  
                    = new SqlParameter("@ToCurrencyCode", SqlDbType.NChar, 3);  
                toCurrencyCodeParameter.Value = toCurrencyCode;  
                command.Parameters.Add(toCurrencyCodeParameter);  
  
                SqlParameter resultParameter  
                    = new SqlParameter("@Result", SqlDbType.Decimal);  
                resultParameter.Precision = 10;  
                resultParameter.Scale = 4;  
                resultParameter.Direction = ParameterDirection.Output;  
                command.Parameters.Add(resultParameter);  
  
                conn.Open();  
                command.ExecuteNonQuery();  
  
                decimal conversionFactor;  
  
                if (resultParameter.Value is decimal)  
                {  
                    conversionFactor = (decimal)(resultParameter.Value);  
                }  
                else  
                {  
                    conversionFactor = 1.0M;  
                    toCulture = USCulture;  
                }  
  
                return new Currency(toCulture, ((decimal)fromAmount * conversionFactor));  
            }  
        }  
    }  
```  
  
 이는 어셈블리를 배포하고 데이터베이스 내에서 저장 프로시저를 만드는 [!INCLUDE[tsql](../../includes/tsql-md.md)] 설치 스크립트(`Install.sql`)입니다.  
  
```  
USE AdventureWorks  
GO  
  
IF EXISTS (SELECT * FROM sys.procedures WHERE [name] = N'usp_LookupConversionRate')  
DROP PROCEDURE [dbo].[usp_LookupConversionRate]  
GO  
  
IF EXISTS (SELECT * FROM sys.types WHERE [name] = N'Currency')   
DROP TYPE Currency;  
GO  
  
IF EXISTS (SELECT [name] FROM sys.assemblies WHERE [name] = N'Currency')  
DROP ASSEMBLY Currency;  
GO  
  
IF EXISTS (SELECT * FROM sys.objects WHERE ([name] = N'ConvertCurrency') AND ([type] = 'FS'))  
DROP FUNCTION ConvertCurrency;  
GO  
  
-- You may need to modify the value of the this variable if you have installed the sample someplace other than the default location.  
DECLARE @SamplesPath nvarchar(1024)  
set @SamplesPath = 'C:\MySample\'  
CREATE ASSEMBLY Currency   
FROM @SamplesPath + 'Currency.dll'  
with permission_set = safe;  
  
USE AdventureWorks  
GO  
  
CREATE TYPE Currency EXTERNAL NAME [Currency].[Currency];  
GO  
  
CREATE FUNCTION ConvertCurrency  
(  
@fromAmount AS money,  
@toCultureName AS nvarchar(10),  
@when as DateTime  
)  
RETURNS Currency  
AS EXTERNAL NAME [Currency].[CurrencyConverter].ConvertCurrency;  
GO  
  
CREATE PROCEDURE usp_LookupConversionRate  
(  
@OnDate datetime,  
@ToCurrencyCode nchar(3),  
@Result decimal(10,4) OUTPUT  
)  
AS  
BEGIN  
--It is not permitted to perform certain side-effects in functions, and  
--SET NOCOUNT is one of them.  Since this sproc is called from   
--the ConvertCurrency CLR UDF, we must not do that side-effect or  
--there will be an error at runtime.  
--SET NOCOUNT ON  
  
SELECT @Result = (SELECT TOP 1 AverageRate FROM Sales.CurrencyRate   
WHERE CurrencyRateDate <= @OnDate AND FromCurrencyCode = N'USD'   
AND ToCurrencyCode = @ToCurrencyCode   
ORDER BY CurrencyRateDate DESC);  
  
IF (@Result IS NULL)  
SELECT @Result = (SELECT TOP 1 AverageRate FROM Sales.CurrencyRate   
WHERE CurrencyRateDate > @OnDate AND FromCurrencyCode = N'USD'   
AND ToCurrencyCode = @ToCurrencyCode  
ORDER BY CurrencyRateDate ASC);  
END;  
  
```  
  
 이는 함수를 실행하여 예제를 테스트하는 `test.sql`입니다.  
  
```  
use AdventureWorks  
GO  
  
DECLARE @TwoBitsEuro Currency;  
SELECT @TwoBitsEuro = dbo.ConvertCurrency(CAST('.25' as money), 'FR-FR', GetDate());  
PRINT '$0.25 in USD is equivalent to ' + @TwoBitsEuro.ToString();  
```  
  
 다음 [!INCLUDE[tsql](../../includes/tsql-md.md)]은 데이터베이스에서 어셈블리, 유형 및 함수를 제거합니다.  
  
```  
USE AdventureWorks  
GO  
  
IF EXISTS (SELECT * FROM sys.procedures WHERE [name] = N'usp_LookupConversionRate')  
DROP PROCEDURE [dbo].[usp_LookupConversionRate]  
GO  
```  
  
## <a name="see-also"></a>참고 항목  
 [공용 언어 런타임 &#40;CLR&#41; 통합에 대한 사용 시나리오 및 예제](../../../2014/database-engine/dev-guide/usage-scenarios-and-examples-for-common-language-runtime-clr-integration.md)  
  
  
