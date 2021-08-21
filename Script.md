local UndercoversGuiLib = Instance.new("ScreenGui")
UndercoversGuiLib.Name = "UndercoversGuiLib"
UndercoversGuiLib.Parent = game.CoreGui

local function MakeUiDraggble(gui)
	local UserInputService = game:GetService("UserInputService")

	local dragging
	local dragInput
	local dragStart
	local startPos

	local function update(input)
		local delta = input.Position - dragStart
		gui.Position = UDim2.new(startPos.X.Scale, startPos.X.Offset + delta.X, startPos.Y.Scale, startPos.Y.Offset + delta.Y)
	end

	gui.InputBegan:Connect(function(input)
		if input.UserInputType == Enum.UserInputType.MouseButton1 or input.UserInputType == Enum.UserInputType.Touch then
			dragging = true
			dragStart = input.Position
			startPos = gui.Position

			input.Changed:Connect(function()
				if input.UserInputState == Enum.UserInputState.End then
					dragging = false
				end
			end)
		end
	end)

	gui.InputChanged:Connect(function(input)
		if input.UserInputType == Enum.UserInputType.MouseMovement or input.UserInputType == Enum.UserInputType.Touch then
			dragInput = input
		end
	end)

	UserInputService.InputChanged:Connect(function(input)
		if input == dragInput and dragging then
			update(input)
		end
	end)
end

local Lib = {}

Lib.AddWindow = function(WindowName,Description)
	local BackroundFrame = Instance.new("ImageLabel")
	local Info_Frame = Instance.new("Frame")
	local GuiName = Instance.new("TextLabel")
	local Game_Supported = Instance.new("TextLabel")
	local Buttons = Instance.new("Frame")
	local Tabs = Instance.new("Folder")

	BackroundFrame.Name = WindowName
	BackroundFrame.Parent = UndercoversGuiLib
	BackroundFrame.BackgroundColor3 = Color3.fromRGB(255, 255, 255)
	BackroundFrame.BackgroundTransparency = 1.000
	BackroundFrame.Position = UDim2.new(0.257999986, 0, 0.224999994, 0)
	BackroundFrame.Size = UDim2.new(0.481999993, 0, 0.550000012, 0)
	BackroundFrame.Image = "rbxassetid://7291988726"

	Info_Frame.Name = "Info_Frame"
	Info_Frame.Parent = BackroundFrame
	Info_Frame.BackgroundColor3 = Color3.fromRGB(255, 255, 255)
	Info_Frame.BackgroundTransparency = 1.000
	Info_Frame.Position = UDim2.new(-3.9795399e-08, 0, 0, 0)
	Info_Frame.Size = UDim2.new(0.256481856, 0, 0.102233633, 0)

	GuiName.Name = "GuiName"
	GuiName.Parent = Info_Frame
	GuiName.BackgroundColor3 = Color3.fromRGB(255, 255, 255)
	GuiName.BackgroundTransparency = 1.000
	GuiName.Size = UDim2.new(1, 0, 0.449999988, 0)
	GuiName.Font = Enum.Font.Code
	GuiName.Text = "Gui Name"
	GuiName.TextColor3 = Color3.fromRGB(255, 255, 255)
	GuiName.TextScaled = true
	GuiName.TextSize = 14.000
	GuiName.TextWrapped = true

	Game_Supported.Name = "Game_Supported"
	Game_Supported.Parent = Info_Frame
	Game_Supported.AnchorPoint = Vector2.new(0, 1)
	Game_Supported.BackgroundColor3 = Color3.fromRGB(255, 255, 255)
	Game_Supported.BackgroundTransparency = 1.000
	Game_Supported.Position = UDim2.new(0, 0, 1, 0)
	Game_Supported.Size = UDim2.new(1, 0, 0.550000012, 0)
	Game_Supported.Font = Enum.Font.Code
	Game_Supported.Text = "Game Name - Supproted"
	Game_Supported.TextColor3 = Color3.fromRGB(255, 255, 255)
	Game_Supported.TextScaled = true
	Game_Supported.TextSize = 14.000
	Game_Supported.TextWrapped = true

	Buttons.Name = "Buttons"
	Buttons.Parent = BackroundFrame
	Buttons.BackgroundColor3 = Color3.fromRGB(88, 88, 88)
	Buttons.BorderSizePixel = 0
	Buttons.Position = UDim2.new(0, 0, 0.0999999717, 0)
	Buttons.Size = UDim2.new(0.256481826, 0, 0.899486423, 0)

	Tabs.Name = "Tabs"
	Tabs.Parent = BackroundFrame
	MakeUiDraggble(BackroundFrame)
	Game_Supported.Text = Description
	GuiName.Text = WindowName
end

Lib.AddTab = function(TabName,WindowName)
	if UndercoversGuiLib:FindFirstChild(WindowName) then
		local CurrentWindow = UndercoversGuiLib[WindowName]
		local Template_Tab = Instance.new("ScrollingFrame")
		local UIListLayout = Instance.new("UIListLayout")

		Template_Tab.Name = TabName
		Template_Tab.Active = true
		Template_Tab.BackgroundColor3 = Color3.fromRGB(255, 255, 255)
		Template_Tab.BackgroundTransparency = 1.000
		Template_Tab.BorderColor3 = Color3.fromRGB(0, 0, 0)
		Template_Tab.BorderSizePixel = 0
		Template_Tab.Position = UDim2.new(0.256000012, 0, 0.100000009, 0)
		Template_Tab.Size = UDim2.new(0.743999898, 0, 0.899486363, 0)
		Template_Tab.Parent = CurrentWindow.Tabs
		Template_Tab.Visible = false

		UIListLayout.Parent = Template_Tab
		UIListLayout.HorizontalAlignment = Enum.HorizontalAlignment.Center
		UIListLayout.SortOrder = Enum.SortOrder.LayoutOrder
		UIListLayout.Padding = UDim.new(0, 20)

		local UIListLayout = Instance.new("UIListLayout")
		local TemplateBtn = Instance.new("TextButton")
		local Roundify = Instance.new("ImageLabel")

		UIListLayout.Parent = CurrentWindow.Buttons
		UIListLayout.HorizontalAlignment = Enum.HorizontalAlignment.Center
		UIListLayout.SortOrder = Enum.SortOrder.LayoutOrder
		UIListLayout.Padding = UDim.new(0, 10)

		TemplateBtn.Name = TabName
		TemplateBtn.Parent = CurrentWindow.Buttons
		TemplateBtn.BackgroundColor3 = Color3.fromRGB(99, 99, 99)
		TemplateBtn.BackgroundTransparency = 1.000
		TemplateBtn.BorderSizePixel = 0
		TemplateBtn.Size = UDim2.new(0.899999976, 0, 0.100000001, 0)
		TemplateBtn.ZIndex = 2
		TemplateBtn.Font = Enum.Font.Code
		TemplateBtn.Text = TabName
		TemplateBtn.TextColor3 = Color3.fromRGB(255, 255, 255)
		TemplateBtn.TextScaled = true
		TemplateBtn.TextSize = 14.000
		TemplateBtn.TextWrapped = true

		Roundify.Name = "Roundify"
		Roundify.Parent = TemplateBtn
		Roundify.Active = true
		Roundify.AnchorPoint = Vector2.new(0.5, 0.5)
		Roundify.BackgroundColor3 = Color3.fromRGB(255, 255, 255)
		Roundify.BackgroundTransparency = 1.000
		Roundify.Position = UDim2.new(0.5, 0, 0.5, 0)
		Roundify.Selectable = true
		Roundify.Size = UDim2.new(1, 0, 1, 0)
		Roundify.Image = "rbxassetid://3570695787"
		Roundify.ImageColor3 = Color3.fromRGB(99, 99, 99)
		Roundify.ScaleType = Enum.ScaleType.Slice
		Roundify.SliceCenter = Rect.new(100, 100, 100, 100)
		Roundify.SliceScale = 0.040

		TemplateBtn.MouseButton1Click:Connect(function()
			for _, tab in pairs(CurrentWindow.Tabs:GetChildren()) do
				tab.Visible = false
			end

			Template_Tab.Visible = true
		end)
	end
end

Lib.AddTextLabel = function(Name,TabName,WindowName)
	if UndercoversGuiLib:FindFirstChild(WindowName) then
		local CurrentWindow = UndercoversGuiLib[WindowName]
		local CurrentTab = CurrentWindow.Tabs:FindFirstChild(TabName)

		if CurrentTab ~= nil then
			local TemplateTextLabel = Instance.new("TextLabel")
			local Roundify = Instance.new("ImageLabel")

			TemplateTextLabel.Name = Name
			TemplateTextLabel.Parent = CurrentTab
			TemplateTextLabel.BackgroundColor3 = Color3.fromRGB(88, 88, 88)
			TemplateTextLabel.BackgroundTransparency = 1.000
			TemplateTextLabel.BorderSizePixel = 0
			TemplateTextLabel.Size = UDim2.new(0.899999976, 0, 0.0500000007, 0)
			TemplateTextLabel.ZIndex = 2
			TemplateTextLabel.Font = Enum.Font.Code
			TemplateTextLabel.Text = Name
			TemplateTextLabel.TextColor3 = Color3.fromRGB(255, 255, 255)
			TemplateTextLabel.TextScaled = true
			TemplateTextLabel.TextSize = 14.000
			TemplateTextLabel.TextWrapped = true

			Roundify.Name = "Roundify"
			Roundify.Parent = TemplateTextLabel
			Roundify.AnchorPoint = Vector2.new(0.5, 0.5)
			Roundify.BackgroundColor3 = Color3.fromRGB(255, 255, 255)
			Roundify.BackgroundTransparency = 1.000
			Roundify.Position = UDim2.new(0.5, 0, 0.5, 0)
			Roundify.Size = UDim2.new(1, 0, 1, 0)
			Roundify.Image = "rbxassetid://3570695787"
			Roundify.ImageColor3 = Color3.fromRGB(88, 88, 88)
			Roundify.ScaleType = Enum.ScaleType.Slice
			Roundify.SliceCenter = Rect.new(100, 100, 100, 100)
			Roundify.SliceScale = 0.040
		end
	end
end

Lib.AddTextButton = function(Name,TabName,WindowName,FunctionToBind)
	if UndercoversGuiLib:FindFirstChild(WindowName) then
		local CurrentWindow = UndercoversGuiLib[WindowName]
		local CurrentTab = CurrentWindow.Tabs:FindFirstChild(TabName)

		if CurrentTab ~= nil then
			local TemplateButton = Instance.new("TextButton")
			local TemplateButton_Roundify_4px = Instance.new("ImageLabel")

			TemplateButton.Name = "TemplateButton"
			TemplateButton.Parent = CurrentTab
			TemplateButton.BackgroundColor3 = Color3.fromRGB(88, 88, 88)
			TemplateButton.BackgroundTransparency = 1.000
			TemplateButton.BorderSizePixel = 0
			TemplateButton.Size = UDim2.new(0.75, 0, 0.0500000007, 0)
			TemplateButton.ZIndex = 2
			TemplateButton.Font = Enum.Font.Code
			TemplateButton.Text = Name
			TemplateButton.TextColor3 = Color3.fromRGB(255, 255, 255)
			TemplateButton.TextScaled = true
			TemplateButton.TextSize = 14.000
			TemplateButton.TextWrapped = true
			TemplateButton.Text = Name

			TemplateButton_Roundify_4px.Name = "TemplateButton_Roundify_4px"
			TemplateButton_Roundify_4px.Parent = TemplateButton
			TemplateButton_Roundify_4px.Active = true
			TemplateButton_Roundify_4px.AnchorPoint = Vector2.new(0.5, 0.5)
			TemplateButton_Roundify_4px.BackgroundColor3 = Color3.fromRGB(255, 255, 255)
			TemplateButton_Roundify_4px.BackgroundTransparency = 1.000
			TemplateButton_Roundify_4px.Position = UDim2.new(0.5, 0, 0.5, 0)
			TemplateButton_Roundify_4px.Selectable = true
			TemplateButton_Roundify_4px.Size = UDim2.new(1, 0, 1, 0)
			TemplateButton_Roundify_4px.Image = "rbxassetid://3570695787"
			TemplateButton_Roundify_4px.ImageColor3 = Color3.fromRGB(88, 88, 88)
			TemplateButton_Roundify_4px.ScaleType = Enum.ScaleType.Slice
			TemplateButton_Roundify_4px.SliceCenter = Rect.new(100, 100, 100, 100)
			TemplateButton_Roundify_4px.SliceScale = 0.040

			if FunctionToBind ~= nil then
				TemplateButton.MouseButton1Click:Connect(FunctionToBind)
			end
		end
	end	
end

Lib.AddToggle = function(Name,TabName,WindowName,FunctionToBind)
	if UndercoversGuiLib:FindFirstChild(WindowName) then
		local CurrentWindow = UndercoversGuiLib[WindowName]
		local CurrentTab = CurrentWindow.Tabs:FindFirstChild(TabName)
		
		if CurrentTab ~= nil then
			getgenv().CurrentToggleValue = false
			local Toggle_Template = Instance.new("ImageLabel")
			local Title = Instance.new("TextLabel")
			local Toggle = Instance.new("TextButton")
			local Toggle_Roundify_4px = Instance.new("ImageLabel")

			Toggle_Template.Name = Name
			Toggle_Template.Parent = CurrentTab
			Toggle_Template.BackgroundColor3 = Color3.fromRGB(255, 255, 255)
			Toggle_Template.BackgroundTransparency = 1.000
			Toggle_Template.Size = UDim2.new(0.400000006, 0, 0.0799999982, 0)
			Toggle_Template.Image = "rbxassetid://3570695787"
			Toggle_Template.ImageColor3 = Color3.fromRGB(88, 88, 88)
			Toggle_Template.ScaleType = Enum.ScaleType.Slice
			Toggle_Template.SliceCenter = Rect.new(100, 100, 100, 100)
			Toggle_Template.SliceScale = 0.040

			Title.Name = "Title"
			Title.Parent = Toggle_Template
			Title.BackgroundColor3 = Color3.fromRGB(255, 255, 255)
			Title.BackgroundTransparency = 1.000
			Title.Size = UDim2.new(0.699999988, 0, 0.300000012, 0)
			Title.Font = Enum.Font.Code
			Title.Text = Name
			Title.TextColor3 = Color3.fromRGB(255, 255, 255)
			Title.TextScaled = true
			Title.TextSize = 14.000
			Title.TextWrapped = true

			Toggle.Name = "Toggle"
			Toggle.Parent = Toggle_Template
			Toggle.BackgroundColor3 = Color3.fromRGB(53, 255, 100)
			Toggle.BackgroundTransparency = 1.000
			Toggle.BorderSizePixel = 0
			Toggle.Position = UDim2.new(0.0299999993, 0, 0.349999994, 0)
			Toggle.Size = UDim2.new(0.200000003, 0, 0.600000024, 0)
			Toggle.ZIndex = 2
			Toggle.Selected = true
			Toggle.Font = Enum.Font.SourceSans
			Toggle.Text = ""
			Toggle.TextColor3 = Color3.fromRGB(0, 0, 0)
			Toggle.TextSize = 14.000

			Toggle_Roundify_4px.Name = "Toggle_Roundify_4px"
			Toggle_Roundify_4px.Parent = Toggle
			Toggle_Roundify_4px.Active = true
			Toggle_Roundify_4px.AnchorPoint = Vector2.new(0.5, 0.5)
			Toggle_Roundify_4px.BackgroundColor3 = Color3.fromRGB(255, 255, 255)
			Toggle_Roundify_4px.BackgroundTransparency = 1.000
			Toggle_Roundify_4px.Position = UDim2.new(0.5, 0, 0.5, 0)
			Toggle_Roundify_4px.Selectable = true
			Toggle_Roundify_4px.Size = UDim2.new(1, 0, 1, 0)
			Toggle_Roundify_4px.Image = "rbxassetid://3570695787"
			Toggle_Roundify_4px.ImageColor3 = Color3.fromRGB(255,0,0)
			Toggle_Roundify_4px.ScaleType = Enum.ScaleType.Slice
			Toggle_Roundify_4px.SliceCenter = Rect.new(100, 100, 100, 100)
			Toggle_Roundify_4px.SliceScale = 0.040
			
			Toggle.MouseButton1Click:Connect(function()
				CurrentToggleValue = not CurrentToggleValue
				if CurrentToggleValue == false then
					Toggle_Roundify_4px.ImageColor3 = Color3.new(255,0,0)
				else
					Toggle_Roundify_4px.ImageColor3 = Color3.new(0,255,0)
				end
			end)
			Toggle.MouseButton1Click:Connect(FunctionToBind)
		end
	end	
end


return Lib;
