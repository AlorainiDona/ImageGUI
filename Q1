function varargout = projectQ1(varargin)

% Initialization code - DO NOT EDIT
gui_Singleton = 1;
gui_State = struct('gui_Name',       mfilename, ...
                   'gui_Singleton',  gui_Singleton, ...
                   'gui_OpeningFcn', @projectQ1_OpeningFcn, ...
                   'gui_OutputFcn',  @projectQ1_OutputFcn, ...
                   'gui_LayoutFcn',  [] , ...
                   'gui_Callback',   []);
if nargin && ischar(varargin{1})
    gui_State.gui_Callback = str2func(varargin{1});
end

if nargout
    [varargout{1:nargout}] = gui_mainfcn(gui_State, varargin{:});
else
    gui_mainfcn(gui_State, varargin{:});
end
% End initialization code - DO NOT EDIT

% Opening Function
function projectQ1_OpeningFcn(hObject, eventdata, handles, varargin)
handles.output = hObject;
handles.originalImage = []; % Initialize originalImage
handles.currentImage = [];  % Initialize currentImage
guidata(hObject, handles);

% Output Function
function varargout = projectQ1_OutputFcn(hObject, eventdata, handles) 
varargout{1} = handles.output;

% Upload Image
function pushbutton1_Callback(hObject, eventdata, handles)
[file, path] = uigetfile({'*.jpg;*.png;*.bmp'}, 'Select an image');
if file
    fullPath = fullfile(path, file);
    a = imread(fullPath);
    axes(handles.axes1);
    imshow(a);
    handles.originalImage = a; 
    handles.currentImage = a;  
    guidata(hObject, handles);
end

% Convert to Grayscale
function pushbutton2_Callback(hObject, eventdata, handles)
if ~isempty(handles.currentImage)
    agray = rgb2gray(handles.currentImage);
    axes(handles.axes1);
    imshow(agray);
    handles.currentImage = agray; 
    guidata(hObject, handles);
end

% Convert to Binary
function pushbutton3_Callback(hObject, eventdata, handles)
if ~isempty(handles.currentImage)
    if size(handles.currentImage, 3) == 3 % Check if image is color (RGB)
        msgbox('Please convert the image to grayscale before binarization.', 'Error', 'error');
        return;
    end
    
    abw = imbinarize(handles.currentImage);
    axes(handles.axes1);
    imshow(abw);
    handles.currentImage = abw; % Save current image
    guidata(hObject, handles);
end

% Reset Image
function pushbutton4_Callback(hObject, eventdata, handles)
if ~isempty(handles.originalImage)
    axes(handles.axes1);
    imshow(handles.originalImage);
    handles.currentImage = handles.originalImage; % Reset current image
    guidata(hObject, handles);
end

% Display Histogram
function pushbutton5_Callback(hObject, eventdata, handles)
if ~isempty(handles.currentImage)
    if size(handles.currentImage, 3) == 1
        imhist(handles.currentImage);
    elseif size(handles.currentImage, 3) == 3
        grayImage = rgb2gray(handles.currentImage);
        imhist(grayImage);
    end
end

% Complement Image
function pushbutton6_Callback(hObject, eventdata, handles)
if ~isempty(handles.currentImage)
    complementedImage = imcomplement(handles.currentImage);
    if size(complementedImage, 3) == 1
        % If the complemented image is already grayscale, display its histogram
        imhist(complementedImage);
    else
        % If the complemented image is binary, convert it to grayscale first
        grayscaleImage = rgb2gray(complementedImage);
        imhist(grayscaleImage);
    end
    axes(handles.axes1);
    imshow(complementedImage);
    handles.currentImage = complementedImage; 
    guidata(hObject, handles);
end

% Apply Edge Detection
function pushbutton7_Callback(hObject, eventdata, handles)
if ~isempty(handles.currentImage)
    if size(handles.currentImage, 3) == 3
        grayImage = rgb2gray(handles.currentImage);
    else
        grayImage = handles.currentImage;
    end
    edgeDetectedImage = edge(grayImage, 'Canny');
    
    % Convert binary edge-detected image to grayscale representation
    grayscaleEdges = uint8(edgeDetectedImage) * 255;
    
    % Display histogram of the grayscale edge-detected image
    imhist(grayscaleEdges);
    
    axes(handles.axes1);
    imshow(edgeDetectedImage);
    handles.currentImage = edgeDetectedImage; 
    guidata(hObject, handles);
end
