.. image:: https://travis-ci.org/python-openxml/python-docx.svg?branch=master
   :target: https://travis-ci.org/python-openxml/python-docx

*python-docx* is a Python library for creating and updating Microsoft Word
(.docx) files.

More information is available in the `python-docx documentation`_.

.. _`python-docx documentation`:
   https://python-docx.readthedocs.org/en/latest/


## add_chart
'''
from docx import Document
from pptx.util import Pt, Inches
from pptx.chart.data import CategoryChartData
from pptx.enum.chart import XL_CHART_TYPE, XL_LEGEND_POSITION, XL_DATA_LABEL_POSITION

document = Document()
chart_data = CategoryChartData()
chart_data.categories = ['East', 'West', 'Midwest']
chart_data.add_series('Series 1', (19.2, 21.4, 16.7))
x, y, cx, cy = Inches(2), Inches(2), Inches(6), Inches(4.5)

chart = document.add_chart(XL_CHART_TYPE.COLUMN_CLUSTERED, x, y, cx, cy, chart_data)

chart.has_legend = True
chart.legend.position = XL_LEGEND_POSITION.BOTTOM
chart.legend.include_in_layout = False

plot = chart.plots[0]
plot.has_data_labels = True
data_labels = plot.data_labels
data_labels.font.size = Pt(13)
data_labels.position = XL_DATA_LABEL_POSITION.OUTSIDE_END

chart.has_title = True
chart_title = chart.chart_title
text_frame = chart_title.text_frame
text_frame.text = 'Title'
paragraphs = text_frame.paragraphs
paragraph = paragraphs[0]
paragraph.font.size = Pt(18)

category_axis = chart.category_axis
category_axis.tick_labels.font.size = Pt(14)

document.save('test.docx')
'''