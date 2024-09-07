# Wave Notifications
New notifier by me\
You have to make it part of your script\
Example:
```
  local Example = Instance.new("Explosion", game.Players.LocalPlayer)
  -- Include WaveNotify
  local TweenService = game:GetService("TweenService")

-- Track the position for stacking notifications
local initialPosition = UDim2.new(0.495, 0, 0.784, 0)
local notificationHeight = 0.195999995 -- Height of the notification
local notificationSpacing = 0.05 -- Space between notifications (can adjust as needed)
local tweenTime = 0.5 -- Duration of the tween animations

-- Adjust the baseOffset to include both height and spacing
local baseOffset = UDim2.new(0, 0, -notificationHeight - notificationSpacing, 0)

-- Store the last position to stack new notifications
local lastPosition = initialPosition

local function waveNotify(title, contents, id)
	-- Gui to Lua
	-- Version: 3.2

	-- Instances:
	local player = game.Players.LocalPlayer
	local playerGui = player:WaitForChild("PlayerGui")
	local screenGui = playerGui:FindFirstChild("ScreenGui")

	if not screenGui then
		screenGui = Instance.new("ScreenGui")
		screenGui.Name = "ScreenGui"
		screenGui.Parent = playerGui
	end

	local WaveNotificationFrame = Instance.new("Frame")
	local UIGradient = Instance.new("UIGradient")
	local UICorner = Instance.new("UICorner")
	local Title = Instance.new("TextLabel")
	local Image = Instance.new("ImageLabel")
	local Contents = Instance.new("TextLabel")
	local WaveDivider = Instance.new("Frame")
	local UIAspectRatioConstraint = Instance.new("UIAspectRatioConstraint")

	-- Properties:
	WaveNotificationFrame.Name = "WaveNotificationFrame"
	WaveNotificationFrame.Parent = screenGui
	WaveNotificationFrame.BackgroundColor3 = Color3.fromRGB(255, 255, 255)
	WaveNotificationFrame.BorderColor3 = Color3.fromRGB(0, 0, 0)
	WaveNotificationFrame.BorderSizePixel = 0
	WaveNotificationFrame.Position = lastPosition
	WaveNotificationFrame.Size = UDim2.new(0.492000014, 0, notificationHeight, 0)
	WaveNotificationFrame.BackgroundTransparency = 1 -- Start as transparent

	UIGradient.Color = ColorSequence.new{
		ColorSequenceKeypoint.new(0.00, Color3.fromRGB(0, 0, 0)),
		ColorSequenceKeypoint.new(1.00, Color3.fromRGB(0, 179, 255))
	}
	UIGradient.Parent = WaveNotificationFrame

	UICorner.Parent = WaveNotificationFrame

	Title.Name = "Title"
	Title.Parent = WaveNotificationFrame
	Title.BackgroundColor3 = Color3.fromRGB(255, 255, 255)
	Title.BackgroundTransparency = 1.000
	Title.BorderColor3 = Color3.fromRGB(0, 0, 0)
	Title.BorderSizePixel = 0
	Title.Position = UDim2.new(0.41315788, 0, 0, 0)
	Title.Size = UDim2.new(0.447769046, 0, 0.188056007, 0)
	Title.Font = Enum.Font.FredokaOne
	Title.Text = title
	Title.TextColor3 = Color3.fromRGB(0, 0, 0)
	Title.TextScaled = true
	Title.TextSize = 14.000
	Title.TextWrapped = true

	Image.Name = "Image"
	Image.Parent = WaveNotificationFrame
	Image.BackgroundColor3 = Color3.fromRGB(255, 255, 255)
	Image.BackgroundTransparency = 1.000
	Image.BorderColor3 = Color3.fromRGB(0, 0, 0)
	Image.BorderSizePixel = 0
	Image.Position = UDim2.new(-6.69844482e-08, 0, -4.99044688e-07, 0)
	Image.Size = UDim2.new(0.268450737, 0, 1.00000024, 0)
	Image.Image = "http://www.roblox.com/asset/?id=" .. id

	Contents.Name = "Contents"
	Contents.Parent = WaveNotificationFrame
	Contents.BackgroundColor3 = Color3.fromRGB(255, 255, 255)
	Contents.BackgroundTransparency = 1.000
	Contents.BorderColor3 = Color3.fromRGB(0, 0, 0)
	Contents.BorderSizePixel = 0
	Contents.Position = UDim2.new(0.369742751, 0, 0.331736207, 0)
	Contents.Size = UDim2.new(0.531176984, 0, 0.564167976, 0)
	Contents.Font = Enum.Font.FredokaOne
	Contents.Text = contents
	Contents.TextColor3 = Color3.fromRGB(0, 0, 0)
	Contents.TextScaled = true
	Contents.TextSize = 14.000
	Contents.TextWrapped = true

	WaveDivider.Name = "WaveDivider"
	WaveDivider.Parent = WaveNotificationFrame
	WaveDivider.BackgroundColor3 = Color3.fromRGB(255, 255, 255)
	WaveDivider.BackgroundTransparency = 0.800
	WaveDivider.BorderColor3 = Color3.fromRGB(27, 42, 53)
	WaveDivider.BorderSizePixel = 0
	WaveDivider.LayoutOrder = 3
	WaveDivider.Position = UDim2.new(0.343404263, 0, 0.265447944, 0)
	WaveDivider.Size = UDim2.new(0.606595635, 0, 0.00636488106, 0)
	WaveDivider.ZIndex = 901

	UIAspectRatioConstraint.Parent = WaveNotificationFrame
	UIAspectRatioConstraint.AspectRatio = 3.725

	-- Tween for showing the notification
	local tweenInfoIn = TweenInfo.new(tweenTime, Enum.EasingStyle.Quad, Enum.EasingDirection.Out)
	local tweenGoalIn = {BackgroundTransparency = 0}
	local tweenIn = TweenService:Create(WaveNotificationFrame, tweenInfoIn, tweenGoalIn)

	tweenIn:Play()

	-- Update the last position for the next notification
	lastPosition = lastPosition + baseOffset

	-- Optional: Tween for hiding the notification after a delay
	wait(5) -- Show notification for 5 seconds
	local tweenInfoOut = TweenInfo.new(tweenTime, Enum.EasingStyle.Quad, Enum.EasingDirection.In)
	local tweenGoalOut = {BackgroundTransparency = 1}
	local tweenOut = TweenService:Create(WaveNotificationFrame, tweenInfoOut, tweenGoalOut)

	tweenOut:Play()
	tweenOut.Completed:Connect(function()
		WaveNotificationFrame:Destroy()
		-- Reset last position after the frame is destroyed
		lastPosition = lastPosition - baseOffset
	end)
end
```

To notify, use ```waveNotify("Your title", "Your text", "Your Image Id")```
