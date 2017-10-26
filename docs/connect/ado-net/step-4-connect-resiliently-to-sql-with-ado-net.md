---
title: "4 단계: ado.net SQL 탄력적 연결할 | Microsoft Docs"
ms.custom: 
ms.date: 08/08/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
dev_langs:
- CSharp
ms.assetid: 9b608b0b-6b38-42da-bb83-79df8c170cd7
caps.latest.revision: 9
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 8985e162d0a1d72d2ca655be26b6c5c1a1607358
ms.contentlocale: ko-kr
ms.lasthandoff: 09/09/2017

---
# <a name="step-4-connect-resiliently-to-sql-with-adonet"></a>4 단계: 탄력적 SQL ado.net 연결

- 이전 문서:&nbsp;&nbsp;&nbsp;[3 단계: ADO.NET을 사용 하 여 SQL에 연결 하는 개념 증명](step-3-proof-of-concept-connecting-to-sql-using-ado-net.md)  

  
이 항목에는 C# 코드 샘플 사용자 지정 다시 시도 논리를 보여 주는 제공 합니다. 재시도 논리는 안정성을 제공합니다. 재시도 논리를 정상적으로 임시 오류 처리 기능은 또는 *일시적인 오류* 프로그램 몇 초 및 다시 시도 대기 하면 되는 경향이 있는 합니다.  
  
일시적인 오류의 원본은 다음과 같습니다.  
  
- 지 원하는 인터넷 네트워킹에는 간략 한 오류가 있습니다.  
- 클라우드 시스템 부하 전송 쿼리할 순간에 해당 리소스를 분산 수도 있습니다.  
  
  
로컬 Microsoft SQL Server에 연결 하기 위한 ADO.NET 클래스 Azure SQL 데이터베이스에 연결할 수도 있습니다. 그러나 자체는 ADO.NET 클래스 모든 견고성 및 프로덕션 환경에서 사용 하는 데 필요한 안정성을 제공할 수 없습니다. 클라이언트 프로그램에는 일시적인 오류를 자동으로 하 고 적절 하 게 복구 하 고 자체적으로 계속 발생할 수 있습니다.  
  
## <a name="step-1-identify-transient-errors"></a>1 단계: 일시적인 오류를 식별 합니다.  
  
프로그램 영구 오류와 일시적인 오류를 구분 해야 합니다. 일시적인 오류는 일시적인 네트워크 문제 등의 짧은 시간 내 지울 수 있는 오류 조건입니다.  프로그램에 잘못 된 대상 데이터베이스 이름의 철자-이 경우 "지정한 데이터베이스가 없습니다. 발견" 오류가 유지 하 고 확률이 없는 짧은 기간 내를 지우는 경우 영구 오류의 예로 것입니다.  
  
일시적인 오류도 분류 되는 오류 번호의 목록에서에서 제공 됩니다. [SQL 데이터베이스 클라이언트 응용 프로그램에 대 한 오류 메시지](http://docs.microsoft.com/azure/sql-database/sql-database-develop-error-messages/)  
  
## <a name="step-2-create-and-run-sample-application"></a>2 단계: 만들기 및 샘플 응용 프로그램 실행  
  
이 샘플.NET Framework 4.5.1을 가정 하거나 이상을 설치 합니다.  C# 코드 샘플 Program.cs 라는 파일 한 개로 구성 됩니다. 해당 코드는 다음 섹션에서 제공 됩니다.  
  
### <a name="step-2a-capture-and-compile-the-code-sample"></a>2.a 단계: 캡처 및 코드 예제  
  
다음 단계에서 예제를 컴파일할 수 있습니다.  
  
1. 에 [무료 Visual Studio Community 버전](https://www.visualstudio.com/products/visual-studio-community-vs), C# 콘솔 응용 프로그램 템플릿에서 새 프로젝트를 만듭니다.  
    - 파일 > 새로 만들기 > 프로젝트 > 설치 > 템플릿 > Visual C# > Windows > 클래식 데스크톱 > 콘솔 응용 프로그램  
    - 프로젝트 이름을 **RetryAdo2**합니다.  
2. 솔루션 탐색기 창을 여십시오.  
    - 프로젝트의 이름이 표시 됩니다.  
    - Program.cs 파일의 이름이 표시 됩니다.  
3. Program.cs 파일을 엽니다.  
4. 다음 코드 블록에 있는 코드와 Program.cs 파일의 내용을 완전히 바꿉니다.  
5. 빌드 메뉴를 클릭 > 솔루션 빌드입니다.  
  
### <a name="step-2b-copy-and-paste-sample-code"></a>2.b 단계: 예제 코드를 복사 및 붙여넣기  
  
이 코드를 프로그램 **Program.cs** 파일입니다.  
  
서버 이름, 암호 및 등에 대 한 문자열 편집 해야 합니다. 라는 메서드에서 이러한 문자열을 찾을 수 있습니다 **GetSqlConnectionStringBuilder**합니다.  
  
참고: 서버 이름에 대 한 연결 문자열은 대상으로 Azure SQL 데이터베이스의 4 가지 문자 접두사를 포함 하기 때문에 **tcp:**합니다. 하지만 Microsoft SQL Server에 연결할 서버 문자열을 조정할 수 있습니다.  
  
  
```CSharp  
    using System;  // C#  
    using CG = System.Collections.Generic;  
    using QC = System.Data.SqlClient;  
    using TD = System.Threading;  
        
    namespace RetryAdo2  
    {  
      public class Program  
      {  
        static public int Main(string[] args)  
        {  
          bool succeeded = false;  
          int totalNumberOfTimesToTry = 4;  
          int retryIntervalSeconds = 10;  
        
          for (int tries = 1;  
            tries <= totalNumberOfTimesToTry;  
            tries++)  
          {  
            try  
            {  
              if (tries > 1)  
              {  
                Console.WriteLine  
                  ("Transient error encountered. Will begin attempt number {0} of {1} max...",  
                  tries, totalNumberOfTimesToTry  
                  );  
                TD.Thread.Sleep(1000 * retryIntervalSeconds);  
                retryIntervalSeconds = Convert.ToInt32  
                  (retryIntervalSeconds * 1.5);  
              }  
              AccessDatabase();  
              succeeded = true;  
              break;  
            }  
        
            catch (QC.SqlException sqlExc)  
            {  
              if (TransientErrorNumbers.Contains  
                (sqlExc.Number) == true)  
              {  
                Console.WriteLine("{0}: transient occurred.", sqlExc.Number);  
                continue;  
              }  
              else  
              {  
                Console.WriteLine(sqlExc);  
                succeeded = false;  
                break;  
              }  
            }  
        
            catch (TestSqlException sqlExc)  
            {  
              if (TransientErrorNumbers.Contains  
                (sqlExc.Number) == true)  
              {  
                Console.WriteLine("{0}: transient occurred. (TESTING.)", sqlExc.Number);  
                continue;  
              }  
              else  
              {  
                Console.WriteLine(sqlExc);  
                succeeded = false;  
                break;  
              }  
            }  
        
            catch (Exception Exc)  
            {  
              Console.WriteLine(Exc);  
              succeeded = false;  
              break;  
            }  
          }  
        
          if (succeeded == true)  
          {  
            return 0;  
          }  
          else  
          {  
            Console.WriteLine("ERROR: Unable to access the database!");  
            return 1;  
          }  
        }  
        
        /// <summary>  
        /// Connects to the database, reads,  
        /// prints results to the console.  
        /// </summary>  
        static public void AccessDatabase()  
        {  
          //throw new TestSqlException(4060); //(7654321);  // Uncomment for testing.  
        
          using (var sqlConnection = new QC.SqlConnection  
              (GetSqlConnectionString()))  
          {  
            using (var dbCommand = sqlConnection.CreateCommand())  
            {  
              dbCommand.CommandText = @"  
    SELECT TOP 3  
        ob.name,  
        CAST(ob.object_id as nvarchar(32)) as [object_id]  
      FROM sys.objects as ob  
      WHERE ob.type='IT'  
      ORDER BY ob.name;";  
        
              sqlConnection.Open();  
              var dataReader = dbCommand.ExecuteReader();  
        
              while (dataReader.Read())  
              {  
                Console.WriteLine("{0}\t{1}",  
                  dataReader.GetString(0),  
                  dataReader.GetString(1));  
              }  
            }  
          }  
        }  
        
        /// <summary>  
        /// You must edit the four 'my' string values.  
        /// </summary>  
        /// <returns>An ADO.NET connection string.</returns>  
        static private string GetSqlConnectionString()  
        {  
          // Prepare the connection string to Azure SQL Database.  
          var sqlConnectionSB = new QC.SqlConnectionStringBuilder();  
        
          // Change these values to your values.  
          sqlConnectionSB.DataSource = "tcp:myazuresqldbserver.database.windows.net,1433"; //["Server"]  
          sqlConnectionSB.InitialCatalog = "MyDatabase"; //["Database"]  
        
          sqlConnectionSB.UserID = "MyLogin";  // "@yourservername"  as suffix sometimes.  
          sqlConnectionSB.Password = "MyPassword";  
          sqlConnectionSB.IntegratedSecurity = false;  
        
          // Adjust these values if you like. (ADO.NET 4.5.1 or later.)  
          sqlConnectionSB.ConnectRetryCount = 3;  
          sqlConnectionSB.ConnectRetryInterval = 10;  // Seconds.  
        
          // Leave these values as they are.  
          sqlConnectionSB.IntegratedSecurity = false;  
          sqlConnectionSB.Encrypt = true;  
          sqlConnectionSB.ConnectTimeout = 30;  
        
          return sqlConnectionSB.ToString();  
        }  
        
        static public CG.List<int> TransientErrorNumbers =  
          new CG.List<int> { 4060, 40197, 40501, 40613,  
          49918, 49919, 49920, 11001 };  
      }  
        
      /// <summary>  
      /// For testing retry logic, you can have method  
      /// AccessDatabase start by throwing a new  
      /// TestSqlException with a Number that does  
      /// or does not match a transient error number  
      /// present in TransientErrorNumbers.  
      /// </summary>  
      internal class TestSqlException : ApplicationException  
      {  
        internal TestSqlException(int testErrorNumber)  
        { this.Number = testErrorNumber; }  
        
        internal int Number  
        { get; set; }  
      }  
    }  
```  
  
###  <a name="step-2c-run-the-program"></a>2.c 단계: 프로그램 실행  
  
  
**RetryAdo2.exe** 실행 파일이 입력 된 매개 변수가 없습니다. .Exe를 실행 합니다.  
  
1. RetryAdo2.exe 바이너리를 컴파일한에 콘솔 창을 엽니다.  
2. RetryAdo2.exe, 입력된 매개 변수 없이 실행 합니다.  
  
  
  
```  
    database_firewall_rules_table   245575913  
    filestream_tombstone_2073058421 2073058421  
    filetable_updates_2105058535    2105058535  
```  
  
  
  
## <a name="step-3-ways-to-test-your-retry-logic"></a>3 단계: 재시도 논리를 테스트 하는 방법  
  
에 여러 가지 방법으로 일시적인 오류를 재시도 논리를 테스트를 시뮬레이션할 수 있습니다.  
  
  
###  <a name="step-3a-throw-a-test-exception"></a>3.a 단계: 테스트 예외를 Throw 합니다.  
  
코드 샘플에 포함 됩니다.  
  
- 라는 작은 두 번째 클래스 **TestSqlException**, 속성 이라는 **번호**합니다.  
- `//throw new TestSqlException(4060);`를 주석 처리 제거 수입니다.  
  
다음 실행의 throw 문 및 recompile 주석, **RetryAdo2.exe** 다음과 유사한 항목을 출력 합니다.  
  
```  
    [C:\VS15\RetryAdo2\RetryAdo2\bin\Debug\]  
    >> RetryAdo2.exe  
    4060: transient occurred. (TESTING.)  
    Transient error encountered. Will begin attempt number 2 of 4 max...  
    4060: transient occurred. (TESTING.)  
    Transient error encountered. Will begin attempt number 3 of 4 max...  
    4060: transient occurred. (TESTING.)  
    Transient error encountered. Will begin attempt number 4 of 4 max...  
    4060: transient occurred. (TESTING.)  
    ERROR: Unable to access the database!  
      
    [C:\VS15\RetryAdo2\RetryAdo2\bin\Debug\]  
    >>  
```  
  
###  <a name="step-3b-retest-with-a-persistent-error"></a>3.b 단계: 영구 오류를 다시 테스트  
  
코드를 증명 하기 위해 오류가 지속 올바르게 제외 하 고 앞의 테스트를 다시 실행 하는 핸들 4060 같은 일시적인 실제 오류 번호를 사용 하지 마십시오. 의미 없는 번호 7654321를 대신 사용 합니다. 이 영구적인 오류로 취급 해야 프로그램과 모든 다시 시도 무시 해야 합니다.  
  
###  <a name="step-3c-disconnect-from-the-network"></a>3.c 단계: 네트워크에서 연결 끊기  
  
1. 클라이언트 컴퓨터는 네트워크에서 분리 합니다.  
    - 데스크톱에 대 한 네트워크 케이블을 분리 합니다.  
    - 랩톱에 대 한 네트워크 어댑터를 해제 하는 키의 함수 조합 키를 누릅니다.  
2. RetryAdo2.exe를 시작 하 고 첫 번째 일시적인 오류를 아마도 11001를 표시 하려면 콘솔을 기다립니다.  
3. RetryAdo2.exe 계속 실행 하는 동안 네트워크에 다시 연결 합니다.  
4. 후속 재시도에 콘솔 보고서 성공 여부를 확인 하십시오.  
  
  
###  <a name="step-2d-temporarily-misspell-the-server-name"></a>2.d 단계: 일시적으로 잘못 입력 한 서버 이름  
  
1. 40615 다른 오류 번호를 일시적으로 추가 **TransientErrorNumbers**를 하 고 다시 컴파일해야 합니다.  
2. 줄에 중단점을 설정: `new QC.SqlConnectionStringBuilder()`합니다.  
3. 사용 하 여 *편집 하며 계속 하기* 기능 의도적으로 잘못 입력 한 서버 이름 아래 몇 줄을 합니다.  
    - 프로그램을 실행 하 고 중단점까지 다시 시도 하도록 합니다.  
    - 40615 오류가 발생합니다.  
4. 맞춤법 오류를 수정 합니다.  
5. 프로그램 실행 및 성공적으로 완료 하도록 합니다.  
6. 40615를 제거 하 고 다시 컴파일하십시오.  
  
## <a name="next-steps"></a>다음 단계  
  
다른 최상의 practicies 및 디자인 지침을 탐색 하려면 방문 [SQL 데이터베이스에 연결: 링크, 모범 사례 및 디자인 지침](http://azure.microsoft.com/documentation/articles/sql-database-connect-central-recommendations/)  

