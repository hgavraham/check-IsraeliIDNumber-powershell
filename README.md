# check-IsraeliIDNumber-powershell
In this code you can verify Israely ID number 

```powershell
function check-IDnumber
{
    param
    (
        [int]$testedID   
    )

    #convert the TestedID numver to string
    [string]$testedID = $testedID.ToString()
    
    #Checking the length of the testedID
    #if less then or equile to 9 digits
    if($testedID.Length -le 9)
    {
        #if the tested id number is less then 9 digits we will add 0 to the lest side util 
        #the testesID numver will be 9 digits
        if($testedID.Length -lt 9)
        {
            $howMuchZeroToAdd = 9 - $testedID.Length
            for($i = 0 ; $i -lt $howMuchZeroToAdd ; $i++)
            {
                $testedID = "0" + $testedID
            }   
        }
        

        $testedIDArray = $testedID.ToCharArray()        
        [int]$multipleTest = 1

        foreach($num in $testedIDArray)
        {
            [string]$num1 = $num.ToString()
            [int]$num2 = [int]::Parse($num1)

            $multipeledNum = $num2 * $multipleTest
            if($multipeledNum -gt 9)
            {
                $nSum = 0
                [string]$nums = $multipeledNum.ToString()
                $numsArray = $nums.ToCharArray()
                foreach($n in $numsArray)
                {
                    [string]$num1 = $n.ToString()
                    [int]$num2 = [int]::Parse($num1)
                    $nSum += $num2
                    #$nSum
                }
                $multipeledNum = $nSum
            }
            
            $sumTheID += $multipeledNum
        
        
            if($multipleTest -eq 1)
                {$multipleTest = 2}
            else
                {$multipleTest = 1}
        }
        
        
        if(($sumTheID / 10) -is [int])
        {
            Write-Host "Your ID number is OK!" -ForegroundColor Green
        }
        else
        {
            Write-Host "Your ID number is Illegal!" -ForegroundColor Red
        } 
    
    }
    #if more then 9 digits
    else
    {
        Write-Host "Too many digits!" -ForegroundColor Red
    }
}

#to run the funcion
#check-IDnumber -testedID XXXXXXXX
```

#### to run the function after you loaded it to your powershel
```powershell
check-IDnumber -testedID XXXXXXXX
```

