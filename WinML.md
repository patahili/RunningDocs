# WinML

## Notes about WinML

### Uses of Windows AI Foundry

There are 3 methods to use Windows AI Foundry:

1. **Windows AI APIs** - "You have cool features, I want to use the features. I'm not the most familiar w/models"
   - For situations where we can swap the model underneath (e.g: change text summarization to use Phi Y vs Phi X) and customer wouldn't be impacted as they use features
   - SDXL and SD swap for same features is also an example of this approach

2. **Windows AI Foundry** - "I know how to build features on top of models, I just want your models so I don't have to worry about finding them"

3. **BYOM (Bring your Own Model) to WinML** - "I want to bring my own models and build my own features, just give me a way to call the NPU with my stuff"
   - Direct use of WinML

## FAQ

### Opens

#### 1. What if I want to go from PyTorch -> ONNX -> IHV Native toolchain -> IR file, basically no QDQ but use IHV quantization methods. How does this violation of requirement get treated?

**A:** Pending answer from Anastasiya

### Resolved FAQ

#### 1. Does WinML require the use of QDQ models as a precursor?

**A:** WinML requires ONNX models, but QDQ is only required for NPU specifically.

#### 2. After we replat AIF, some ORT clients such as live translations and studio effects will still execute work on NPU using older EP. So we will have some work via new EP and some work via old EP. Are there any EP/EP or EP/Driver conflicts we need to be concerned about?

**A:** No. Those will be different workload host and other processes.
