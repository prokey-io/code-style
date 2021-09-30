
# Coding style for Angular
## General Angular coding style guide
For all following topics, please check [Angular coding style guide](https://angular.io/guide/styleguide)
- Folders and File structure
- File naming
- Component/Service/Pipe/Unit test/ naming
- Application structure
- Services/Components 
## Prokey recommended code style for Angular projects
- If a varialble is not used in HTML, use 'underscore' before variable name as below, using 'private' keyword is optional:
```
private _camelCaseVariableName: type = value;
_anotherVariable = value;
_maxRowCount: number = 15; 
```
  
- Do not mix the variables are using in HTML with other variables
```
*** AVOID MIXING VARIABLES ***
_maxRowCount: number = 15;
coinModel: CoinModel;
_coinName: string;
```
instead of above 🛑 code style, use the following :+1: code style:
```
*** SEPERATE VARIABLES ***
// Private variables
_maxRowCount: number = 15;
_coinName: string;

// ViewModels variables that are using in HTML 
selectedCoinName: string = "BTC";

```
- If each parameter of a function need a comment, pass the parameters in seperate lanes and write the comment in front of each parameter otherwise don't use white space for each parameter if there is enough space for a function parameter:
```
*** AVOID CALLING FUNCTIONS LIKE THIS IF THERE IS NO COMMENT FOR EACH PARAMETERS ***
CalculateTxFee(
    output,
    accountNumber
    );
```
instead of above function calling, use the following styles:
```
CalculateTxFee(output, accountNumber);

OR

CalculateTxFee(
    output, // output model includes address and amount
    accountNumber // wallet account number to check the balance and utxo
    );

```
- Write comment to explain the code especially when it's seems complex for someone else who is going to join the team or see the code for first time:
```
   /**
   * This function will be called when the input amount changed
   * The current price and the fee should be updated
   * Send max also will be cancelled if the input changed manually
   */
  onInputAmountChanged() {
      this.setCoinPrice();

      // Re-calculate tx fee again based on the value to be sent
      this.calculateFee();

      // Remove the high fee error 
      this.isFeeMoreThanBalanceErrorView = false;

      // Once user edit the value manually, send max should be cancelled
      this.isMaxRequested = false;
  }
```
- Avoid using 'any' type as much as possible
- Don't leave the function return type undefined because it will be 'any'
- You better to define the type of variable when you calling a function, this helps compiler to show errors if return value is mismatched:
```
const aVariable: TypeOfVariable = foo();
```
- Consider using these styles for blocks:
```
if( condition1 && consition2 ) {
}

OR

if( condition1 && // comments
    consition2 // comments
){

}
```
- Better to seperate logics of a functions code using a white line:
```
*** AVOID CODING LIKE THIS***
async onChangeFee(name:string){
    this.enableFeeButton=true;
    this.UpdateUi();
    if(name=="economy"){
      this.showEconomySign=true;
    }
    this.selectedFee = name;
    if(this.isMaxRequested){
      await this.onGetMaxAccountAmount();
    } 
  }
```
use spaces can help the code readability:
```
async onChangeFee(name: string) {
    this.enableFeeButton = true;
    
    this.UpdateUi();
    
    if(name == "economy") {
      this.showEconomySign=true;
    }
    
    this.selectedFee = name;
    
    if(this.isMaxRequested){
      await this.onGetMaxAccountAmount();
    } 
  }
```
- If more than 3 classes/models are imported from a file, better to write each on them in seperate lines:
```
import {
    RefTransaction,
    TransactionInput,
    TransactionOutput,
    EnumOutputScriptType,
    AddressModel,
} from '../models/Prokey';
```

