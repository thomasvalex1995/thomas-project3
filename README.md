# thomas-project3
local M = {}
function M.exec(opt, cacheFile)
  local imageInfo = {}
  -- preprocess dataset, store results in imageInfo, save to cacheFile
  torch.save(cacheFile, imageInfo)
end
return M
dataset.lua
The dataset.lua should return a class that implements three functions:

get(i): returns a table containing two entries, input and target
input: the training or validation image as a Torch tensor
target: the image category as a number 1-N
size(): returns the number of entries in the dataset
preprocess(): returns a function that transforms the input for data augmentation or input normalization
local M = {}
local FakeDataset = torch.class('resnet.FakeDataset', M)

function FakeDataset:__init(imageInfo, opt, split)
  -- imageInfo: result from dataset-gen.lua
  -- opt: command-line arguments
  -- split: "train" or "val"
end

function FakeDataset:get(i)
  return {
    input = torch.Tensor(3, 800, 600):uniform(),
    target = 42,
  }
end

function FakeDataset:size()
  -- size of dataset
  return 2000 
end

function FakeDataset:preprocess()
  -- Scale smaller side to 256 and take 224x224 center-crop
  return t.Compose{
    t.Scale(256),
    t.CenterCrop(224),
  }
end

return M.FakeDataset
